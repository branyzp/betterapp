<script>
	import { onMount, onDestroy } from "svelte";
	import Chart from "chart.js/auto";

	let chartCanvas;
	let chartInstance;

	export let weightData = [];

	// Function to initialize the chart
	const initializeChart = () => {
		chartInstance = new Chart(chartCanvas, {
			type: "line",
			data: {
				labels: weightData.map((entry) => entry.date),
				datasets: [
					{
						label: "Weight (kg)",
						data: weightData.map((entry) => entry.weight),
						borderColor: "rgb(75, 192, 192)",
						backgroundColor: "rgba(75, 192, 192, 0.2)",
						tension: 0.3,
					},
				],
			},
			options: {
				responsive: true,
				plugins: {
					legend: {
						display: true,
					},
				},
			},
		});
	};

	// Function to update the chart
	const updateChart = () => {
		if (chartInstance) {
			chartInstance.data.labels = weightData.map((entry) => entry.date);
			chartInstance.data.datasets[0].data = weightData.map((entry) => entry.weight);
			chartInstance.update();
		}
	};

	// Initialize chart on mount
	onMount(() => {
		initializeChart();
	});

	// Update chart when weightData changes
	$: weightData, updateChart();

	// Cleanup chart instance on component destroy
	onDestroy(() => {
		if (chartInstance) {
			chartInstance.destroy();
		}
	});
</script>

<div class="p-4 bg-white rounded-lg shadow-md">
	<h2 class="text-lg font-semibold mb-2">Weight Progress Over Time</h2>
	<canvas bind:this={chartCanvas}></canvas>
</div>