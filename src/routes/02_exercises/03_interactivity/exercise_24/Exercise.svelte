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
    // console.log(data)

    console.log(continentSelected)
    console.log(indexYearSelected)


    const data2 = data[indexYearSelected]?.countries.filter((entry )=> {
      return entry.continent == continentSelected
    })

    // console.log(data2)
    console.log(data[indexYearSelected]?.countries);
  });

 
  
</script>

{#if !data}
  <p>Loading the data, please wait...</p>
{:else}
  <div>
    <Scatterplot data={data[indexYearSelected]?.countries.filter((entry )=> {
      return entry.continent == continentSelected
    })} />
    <Controls {data} bind:slider_value={indexYearSelected} bind:selected_continent = {continentSelected} />
    <!-- {data2} -->
    {continentSelected}
    <!-- {console.log(data[indexYearSelected]?.countries} -->
  </div>
{/if}
