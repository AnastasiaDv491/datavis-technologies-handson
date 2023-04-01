<script>
    import * as d3 from "d3";
    import {scaleOrdinal, scaleLinear, scaleBand} from "d3-scale";
    // Dimensions
    const width = 600;
    const height = 300;
    const margin = { top: 10, right: 10, bottom: 30, left: 60 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
  
    // Array
    const data = [
      { service: "Netflix", viewers: 2.9 },
      { service: "Amazon Prime Video", viewers: 1.3 },
      { service: "Disney+", viewers: 2.1 },
      { service: "Hulu", viewers: 0.9 },
      { service: "Apple TV", viewers: 1.1 },
      { service: "Rakuten", viewers: 0.4 }
    ];

    const uniques = [...new Set(data.map(v => v.service))]

    let xScale = scaleBand()
      .domain(uniques)
      .range([0, innerWidth])
    let yScale = scaleLinear()
      .domain([0,3])
      .range([innerHeight,0])

    console.log(uniques);
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
  
  <!-- setting a viewBox and max-width allows the SVG to shrink but not grow! -->
  <svg viewbox="0 0 {width} {height}" style="max-width: {width}px">
    <g transform={`translate(${margin.left},${margin.top})`}>
      <g transform="translate(20,{innerHeight})">
        <g class="x-axis" bind:this={xAxis}></g>
      </g>
      
      <g transform="translate(20, 0)">
        <g class="y-axis" bind:this={yAxis}></g>
  
      </g> 
      <g transform="translate(40, 0)">
      {#each data as item}
      <rect x="{xScale(item.service)}" y="{innerHeight-yScale(item.viewers)}" width="50" height="{yScale(item.viewers)}" />

      {/each}
      </g>
    </g>
  </svg>
  