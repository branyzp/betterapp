<script>
	import '../app.css'
</script>

<nav class="bg-gray-800 text-white p-4">
	<div class="container mx-auto flex justify-between">
		<a href="/">Home.</a>
		<a href="/about">About.</a>
		<a href="/bmrcalculator">BMR Calculator.</a>
		<a href="/routines">Workout Routines.</a>
	</div>
</nav>

<main>
	<slot />
</main>

<footer class="bg-gray-800 text-white p-4 text-center">
	© 2025 Better.app - All rights reserved.
</footer>