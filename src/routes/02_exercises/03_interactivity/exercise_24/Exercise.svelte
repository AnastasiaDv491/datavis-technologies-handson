<script>
  import { json } from "d3-fetch";
  import { onMount } from "svelte";

  import Controls from "./Controls.svelte";
  import Scatterplot from "./Scatterplot.svelte";

  let indexYearSelected;
  let continentSelected;
  
  // Load the data
  let data = null;

  onMount(async () => {
    data = await json("/data/gapminder.json");
    const data2 = data[indexYearSelected]?.countries.filter((entry )=> {
      return entry.continent == continentSelected
    })
  });
</script>

{#if !data}
  <p>Loading the data, please wait...</p>
{:else}
  <div>
    {#if continentSelected == "all"}
    <Scatterplot data={data[indexYearSelected]?.countries}/>
    {:else}
    <Scatterplot data={data[indexYearSelected]?.countries.filter((entry )=> {
      return entry.continent == continentSelected
    })} />
    {/if}
    <Controls {data} bind:slider_value={indexYearSelected} bind:selected_continent = {continentSelected} />
  </div>
{/if}
