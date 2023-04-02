<script>
    import { scaleLinear, scaleSqrt } from "d3-scale";
    import * as d3 from "d3";


    // import data from "d3-selection/src/selection/data";
    // Dimensions
    const [height, width] = [400, 600];
    const margin = { top: 50, right: 5, bottom: 55, left: 50 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
    export let dataExcercise;

    var accent = d3.scaleOrdinal(d3.schemeDark2);

    let xScale = scaleLinear()
      .domain([0,5000])
      .range([0, innerWidth])
    let yScale = scaleLinear()
      .domain([0,60])
      .range([innerHeight,0])
    let populationRadius = scaleLinear()
    .domain([0,421675014])
    .range([0,40])

    
      let xAxis, yAxis
      $: {
        d3.select(xAxis).selectAll("*").remove()
        d3.select(xAxis).call(d3.axisBottom(xScale))
      }
      $: {
        d3.select(yAxis).selectAll("*").remove()
        d3.select(yAxis).call(d3.axisLeft(yScale))
      }
  </script>
  
  {#if dataExcercise}

    
    <svg viewBox="0 0 {width} {height}" style="max-width: {width}px">
      <g transform="translate({margin.left}, {margin.top})">
        <text transform = "translate(0,-20)">Life exp based on level of income</text>
        <g transform="translate(20,{innerHeight})">
          <g class="x-axis" bind:this={xAxis}></g>
        </g>
        
        <g transform="translate(20, 0)">
          <g class="y-axis" bind:this={yAxis}></g>
    
        </g> 
        <g transform = "rotate(-90) translate(-120, -20)">
          <text>Life exp</text>
        </g>
        <g transform = " translate(200,330)">
          <text>Income</text>
        </g>
        <g transform="translate(20, 0)">
         
        {#each dataExcercise[0].countries as dataCountry}
        
        <circle cx="{xScale(+dataCountry.income)}" cy="{yScale(+dataCountry.life_exp)}" 
        r={populationRadius(+dataCountry.population)}
        fill={accent(dataCountry.continent)}></circle>
        {/each}
      </g>

      </g>
    </svg>

{:else}
 <h3>Data is loading...</h3>
{/if}

  