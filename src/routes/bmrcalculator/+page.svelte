<script>
	// Form Data
	let age = "30";
	let height = "175";
	let weight = "70";
	let gender = "male";
	let activity = "sedentary";
	let goal = "maintain weight"
	let action = "";
	let tdee = null;
	let goalkcal = null;
	let bmr = null;

	function calculateBMR() {
		let h = parseFloat(height);
		let w = parseFloat(weight);
		let a = parseFloat(age);

		if ((isNaN(h) || isNaN(w)) || isNaN(a)) {
			bmr = "Please enter valid numbers for height/weight/age."
			return;
		}
		if (gender === "male") {
			bmr = 88.36 + (13.4 * w) + (4.8 * h) - (5.7 * a);
		} else if (gender === "female") {
			bmr = 447.6 + (9.2 * w) + (3.1 * h) - (4.3 * a);
		}
		switch (activity) {
			case "sedentary":
				tdee = bmr * 1.2;
				break;
			case "lightly active":
				tdee = bmr * 1.375;
				break;
			case "moderately active":
				tdee = bmr * 1.55;
				break;
			case "very active":
				tdee = bmr * 1.725;
		}
		switch (goal) {
			case "lose fat":
				goalkcal = tdee - 500;
				action = "deficit of 500kcal";
				break;
			case "maintain weight":
				goalkcal = tdee;
				action = "maintenance";
				break;
			case "gain muscle":
				goalkcal = tdee + 500;
				action = "surplus of 500kcal";
				break;
		}
	}
</script>

<div class="min-h-screen flex flex-col items-center justify-center bg-gray-100">
	<h1 class="text-4xl text-gray-800">BMR Calculator.</h1>
	<h2 class="mt-4 text-2xl text-gray-600">
		Basic Metabolic Rate <br>
	</h2>
	<p class="mt-1 text-sm text-gray-500">the minimum amount of energy utilized by the body while at <span class="underline">rest</span>.</p>
		<div class="mt-6 shadow-2xl p-10 rounded-3xl bg-white shadow-gray-400">
			<form on:submit|preventDefault={calculateBMR} class="space-y-4">
				<div class="flex flex-row gap-4" >
					<div class="flex-1/2 w-5">
						<!-- Age -->
						<label class="text-sm text-gray-700">Age (years)
							<input type="number" bind:value={age} class="mt-1 w-full p-2 border rounded-lg focus:ring focus:ring-blue-300" required />
						</label>

						<!-- Height -->
						<label class="text-sm text-gray-700">Height (cm)
							<input type="number" bind:value={height} class="mt-1 w-full p-2 border rounded-lg focus:ring focus:ring-blue-300" required />
						</label>

						<!-- Weight -->
						<label class="text-sm text-gray-700">Weight (kg)
							<input type="number" bind:value={weight} class="mt-1 w-full p-2 border rounded-lg focus:ring focus:ring-blue-300" required />
						</label>
					</div>

					<div class="flex-1/2">
						<!-- Gender -->
						<label class="text-sm text-gray-700">Gender
							<select bind:value={gender} class="mt-1 w-full p-2 border rounded-lg focus:ring focus:ring-blue-300">
								<option value="male">Male</option>
								<option value="female">Female</option>
							</select>
						</label>

						<!-- Activity -->
						<label class="text-sm text-gray-700">Activity Level
							<select bind:value={activity} class="mt-1 w-full p-2 border rounded-lg focus:ring focus:ring-blue-300">
								<option value="sedentary">Sedentary</option>
								<option value="lightly active">Exercise 1-3 times/week</option>
								<option value="moderately active">Exercise 4-5 times/week</option>
								<option value="very active">Exercise daily</option>
							</select>
						</label>

						<!-- Goal -->
						<label class="text-sm text-gray-700">Goal
							<select bind:value={goal} class="mt-1 w-full p-2 border rounded-lg focus:ring focus:ring-blue-300">
								<option value="lose fat">Lose fat</option>
								<option value="maintain weight">Maintain</option>
								<option value="gain muscle">Gain muscle</option>
							</select>
						</label>
					</div>
				</div>
				<div class="text-center">
					<!-- Submit Button -->
					<button type="submit" class="w-max mt-4 bg-gray-800 text-white px-6 py-3 rounded-lg shadow hover:bg-gray-600 transition">
						Calculate
					</button>
				</div>
			</form>

			<!-- Display BMR Result -->
			{#if bmr !== null}
				<div class="mt-6 text-center p-4 bg-gray-200 rounded-lg">
					<p class="text-md">Your BMR: <span class="text-green-800">{bmr.toFixed(0)}</span> kcal/day</p>
					<p class="text-md">as your activity level is <span class="text-green-800">{activity}</span>, your total daily energy expenditure is <span class="text-green-800">{tdee.toFixed(0)}</span> kcal/day</p>
					<p class="text-md">to <span class="text-green-800">{goal}</span>, aim for caloric {action} for a goal of <span class="text-green-800">{goalkcal.toFixed(0)}</span> kcal/day </p>
				</div>
			{/if}
		</div>
</div>