<script>
    import { onMount, afterUpdate } from "svelte";
    import Chart from "chart.js/auto";

    export let productivityData = [];

    let chartCanvas;

    let chartInstance = null;

    const renderChart = () => {
        if (chartInstance) {
            chartInstance.destroy();
        }

        chartInstance = new Chart(chartCanvas, {
            type: 'doughnut',
            data: {
                labels: ['Learning/Practice Time', 'Stretching/Yoga Duration', 'Hydration Levels'],
                datasets: [{
                    label: 'Productivity Breakdown',
                    data: productivityData,
                    backgroundColor: ['yellow', 'blue', 'green'],
                    hoverOffset: 4
                }]
            },
            options: {
                responsive: true,
                plugins: {
                    legend: {
                        position: 'top',
                    },
                    tooltip: {
                        callbacks: {
                            label: function (tooltipItem) {
                                return tooltipItem.label + ': ' + tooltipItem.raw ;
                            }
                        }
                    }
                }
            }
        });
    };

    onMount(() => {
        renderChart();
    });

    afterUpdate(() => {
        renderChart();
    });
</script>

<canvas bind:this={chartCanvas}></canvas>

<style>
    canvas {
        max-width: 100%;
        margin: 0 auto;
    }
</style>
