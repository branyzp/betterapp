<script>
	import { writable } from "svelte/store";
	import { slide } from "svelte/transition";

	// FAQ Data
	let nutritionFAQs = [
		{ question: "How do I track my progress?", answer: "For weight loss or muscle gain goals, take weekly progress pictures and weight measurements. If the weight doesn't drop, but you're getting leaner, it's progress. Scale weight does not determine body fat percentages nor does BMI. If you are increasing in strength, that's a good sign that you are progressing as well. " },
		{ question: "What is the best diet for fat loss?", answer: "A diet sustainable to your personal tastes along with caloric deficit is the best diet for weight loss. If you eat boiled chicken breasts and that's your thing, good for you. If that makes you sick and it's not sustainble then you won't be able to continue the diet for long without sacrificing your mental health, then it's not good. It's individual preference, really. I personally do keto." },
		{ question: "How much protein do I need?", answer: "There is a guideline that I believe everyone should follow, for fat loss, muscle gain or to perform body recomposition (lose fat and gain muscle while at weight maintenance) and that is 2.2 - 2.5g of protein per kilogram of lean muscle mass that you are targeting to have. This means that if you are 70kg with a body fat of 20%, your lean mass is roughly 56kg and you should target for 140g of protein." },
		{ question: "Are there any issues with eating more protein?", answer: "First of all, consult your doctor, but from my personal experience as well as reading others' experiences, even eating upwards of 200g of protein a day has no ill-effects provided you are consuming enough water to allow your kidneys to process the protein effectively and eliminate urea." },
		{ question: "What are the benefits of protein?", answer: "Consumption of high-protein in your diet has several benefits. Muscle growth and repair, fat loss and metabolism boosting effects, increased satiety and reduced hunger, better body composition, improved bone health and strength, enhanced recovery and performance, stabilized blood sugar and reduced cravings for sugar, health hair, skin and nails. The list goes on." },];

	let workoutFAQs = [
		{ question: "How do I start?", answer: "Like Nike says, Just Do It." },
		{ question: "How do I progress?", answer: "Progressive overload is the name of the game. As long as you're gradually progressing in either reps per set, or weight, you're bound to gain muscle. (provided you're eating and sleeping enough)" },
		{ question: "Can I customize my workout plans?", answer: "Definitely. You can create and adjust your workout routines based on your goals. However, the workout builder provides a template and focuses on compound movements that target multiple muscles at once. The benefits of compound movements include greater functional strength, effectiveness to time ratio as well as overall being the greatest bang for your buck exercises. We do include some isolated movements as well for hypertrophy and reduction in muscle imbalances." },
	]

	let openNutritionIndex = writable(null);
	let openWorkoutIndex = writable(null);

	function toggleN(index) {
		openNutritionIndex.update(current => (current === index ? null : index));
	}
	function toggleW(index) {
		openWorkoutIndex.update(current => (current === index ? null : index));
	}
</script>
<div class="min-h-screen bg-gray-100">
<div class="min-h-screen max-w-2xl mx-auto flex flex-col justify-center">
	<h2 class="text-3xl text-center mb-4">Frequently Asked Questions</h2>
	<h3 class="text-2xl text-center font-bold">Nutrition</h3>
	{#each nutritionFAQs as faq, index}
		<div class="mb-2 border-b">
			<button
				class="w-full text-left p-3 font-medium text-lg flex justify-between items-center"
				on:click={() => toggleN(index)}
			>
				{faq.question}
				<span class="transform transition-transform" class:rotate-180={$openNutritionIndex === index}>▼</span>
			</button>

			{#if $openNutritionIndex === index}
				<p class="p-3 text-gray-700" transition:slide>{faq.answer}</p>
			{/if}
		</div>
	{/each} <br>
	<h3 class="text-2xl text-center font-bold">Workout</h3>
	{#each workoutFAQs as wfaq, index}
		<div class="mb-2 border-b">
			<button
				class="w-full text-left p-3 font-medium text-lg flex justify-between items-center"
				on:click={() => toggleW(index)}
			>
				{wfaq.question}
				<span class="transform transition-transform" class:rotate-180={$openWorkoutIndex === index}>▼</span>
			</button>

			{#if $openWorkoutIndex === index}
				<p class="p-3 text-gray-700" transition:slide>{wfaq.answer}</p>
			{/if}
		</div>
	{/each}
</div>
</div>