<script>
	import {goto} from '$app/navigation';
</script>

<div class="min-h-screen flex flex-col items-center justify-center bg-gray-100">
	<h1 class="text-4xl text-gray-800">About.</h1>
	<h2 class="mt-4 text-2xl text-gray-600">
		Better <br>
		<span class="text-sm">/ˈbɛtə/</span>
		<span class="text-sm italic">verb</span>
	</h2>
	<p class="mt-1 text-md">to improve upon or surpass. <br> <span class="text-sm text-gray-500">"Being better than yesterday"</span></p>
	<p class="mt-4 text-md text-gray-600">
	</p>
	<p class="mt-4 text-md text-gray-600">
		This is a personal project using SvelteKit, Vite, and TailwindCSS. <br/>
		Original project built in 2022 	<a class="text-blue-800" href="https://calorition.vercel.app/">here</a>.
	</p>
	<button
		class="mt-4 bg-gray-800 text-white px-6 py-3 rounded-lg shadow hover:bg-gray-600 transition"
		on:click={() => goto('/')}
	>
		Workout Routines
	</button>
	<button
		class="mt-4 bg-gray-800 text-white px-6 py-3 rounded-lg shadow hover:bg-gray-600 transition"
		on:click={() => goto('/bmrcalculator')}
	>
		BMR Calculator
	</button>
</div>