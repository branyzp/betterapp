<script>
import { goto } from '$app/navigation';
</script>

<div class="min-h-screen flex flex-col items-center justify-center bg-gray-100">
	<div class="text-center">
		<h1 class="text-4xl">
			Welcome to Better.
		</h1>
		<button
			class="mt-4 bg-gray-800 text-white px-6 py-3 rounded-lg shadow hover:bg-gray-600 transition"
			on:click={() => goto('/about')}
		>
			Start here.
		</button>

	</div>
</div>