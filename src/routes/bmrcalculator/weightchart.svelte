<script>
	import { onMount, afterUpdate, onDestroy } from "svelte";
	import Chart from "chart.js/auto";

	let chartCanvas;
	let chartInstance;

	// let weightData = [
	// 	{ date: "2024-03-01", weight: 75 },
	// 	{ date: "2024-03-10", weight: 76 },
	// 	{ date: "2024-03-20", weight: 77 },
	// 	{ date: "2024-03-30", weight: 78 },
	// ];

	export let weightData = [];
	// Reactive statement to update the chart when weightData changes
	$: {
		if (chartInstance) {
			updateChart();
		}
	}

	// Function to update the chart
	const updateChart = () => {
		if (chartInstance) {
			chartInstance.data.labels = weightData.map((entry) => entry.date);
			chartInstance.data.datasets[0].data = weightData.map((entry) => entry.weight);
			chartInstance.update();
		}
	};

	onMount(() => {
		if (chartInstance) {
			chartInstance.destroy();
		}

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

		// Cleanup chart instance on component destroy
		onDestroy(() => {
			if (chartInstance) {
				chartInstance.destroy();
			}
		});
	});
</script>

<div class="p-4 bg-white rounded-lg shadow-md">
	<h2 class="text-lg font-semibold mb-2">Weight Progress Over Time</h2>
	<canvas bind:this={chartCanvas}></canvas>
</div>