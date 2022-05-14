<script lang="ts">
  import Line from "svelte-chartjs/src/Line.svelte"
  // chart should look something like this:
  // y-axis should be profit
  // x-axis should be wigets (0-30)
  // 2 lines: profit w/out wiget maker and w/ widget maker

  let widgetWithoutMakerCost = 5
  let widgetWithMakerCost = 3
  let widgetMakerCost = 20
  let widgetRetailValue = 6

  $: data = {
    labels: Array(31).fill(0).map((_, i) => i), // 0-30 using array fill trick
    datasets: [{
      label: 'Cost (without wiget maker)',
      backgroundColor: 'rgb(255, 99, 132)',
      borderColor: 'rgb(255, 99, 132)',
      data: Array(31).fill(0).map((_, i) => (widgetRetailValue * i) - (widgetWithoutMakerCost * i)),
    }, {
      label: 'Cost (with wiget maker)',
      backgroundColor: 'rgb(28, 188, 237)',
      borderColor: 'rgb(28, 188, 237)',
      data: Array(31).fill(0).map((_, i) => (widgetRetailValue * i) - (widgetWithMakerCost * i) - widgetMakerCost),
    }]
  }

</script>
<h1 class="text-6xl text-center m-4">Widget Maker</h1>
<h2 class="text-3xl text-center">Configure</h2>
<div class="mx-auto w-1/2 my-2 border-gray-300 border p-5">
  <span class="text-lg text-gray-600">Widget Cost (without maker)</span>
  <input class="block border-b border-gray-400" min=0 type="number" placeholder = "Widget Cost (without maker)" bind:value={widgetWithoutMakerCost} />
  <span class="text-lg text-gray-600">Widget Cost (with maker)</span>
  <input class="block border-b border-gray-400" min=0 type="number" placeholder = "Widget Cost (with maker)" bind:value={widgetWithMakerCost} />
  <span class="text-lg text-gray-600">Widget Maker Cost</span>
  <input class="block border-b border-gray-400" min=0 type="number" placeholder = "Widget Maker Cost" bind:value={widgetMakerCost} />
  <span class="text-lg text-gray-600">Widget Retail Value</span>
  <input class="block border-b border-gray-400" min=0 type="number" placeholder = "Widget Retail Value" bind:value={widgetRetailValue} />
</div>
<div class="flex justify-center items-center">
  <Line {data} width={600} height={400} options={{ responsive: false, maintainAspectRatio: false}}/>
</div>