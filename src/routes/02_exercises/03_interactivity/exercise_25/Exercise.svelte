<script>
  import { csv } from "d3-fetch";
  import { onMount } from "svelte";
  import Scatter from "./Scatterplot.svelte";

  // Load the data
  let data = null;
  
  export let pointsSelectedInBoth =[];
  let selectedPoints1;
  let selectedPoints2;

  onMount(async () => {
    data = await csv("/data/cars-2.csv");
    let counter = 0;
    data.forEach((d) => {
      d["id"] = counter
      counter++;
    });
  });

  // Configurations
  const s1 = {
    x: (d) => +d.Horsepower,
    y: (d) => +d.Acceleration,
    xLabel: "Horsepower",
    yLabel: "Acceleration",
  };
  const s2 = {
    x: (d) => +d.Displacement,
    y: (d) => +d.Miles_per_Gallon,
    xLabel: "Displacement",
    yLabel: "Miles per Gallon",
  };

  function checkPoints(){
    for (let index = 0; index < data?.length; index++) {
    if(selectedPoints1[index] == selectedPoints2[index]){
      pointsSelectedInBoth[index] = true
    }
    else{
      pointsSelectedInBoth[index] = false
    }
    
  }
  }
  $: selectedPoints1, selectedPoints2, checkPoints(),console.log(pointsSelectedInBoth)


</script>

{#if !data}
  <p>Loading the data, please wait...</p>
{:else}
  <div class="d-flex justify-content-around">
    <Scatter {data} {...s1} bind:pointsSelected = {selectedPoints1} {pointsSelectedInBoth}/>
    <Scatter {data} {...s2} bind:pointsSelected = {selectedPoints2} {pointsSelectedInBoth}/>
  </div>
{/if}
