<script>
  import {axisBottom} from "https://cdn.skypack.dev/d3-axis@3";
  import select from "https://cdn.skypack.dev/d3-selection@3";
  import { scaleLog} from 'd3-scale';

  // Dimensions
    const width = 800;
    const height = 100;
    const margin = { top: 5, right: 5, bottom: 25, left: 5 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;

    // Array    
    const values = [2, 4, 6, 7, 9];
    const Log = scaleLog()
      .domain([1,100])
      .range([1,800])

    let axisGen = d3.axisBottom(Log)
    let xAxis = d3.select("g")

  </script>
  
  <svg  viewBox="0 0 {width} {height}">
    <g >
      {#each values as value}

      <circle cx = {Log(value)}
      cy = 10
              r = 10/>
      {/each}
    </g>
</svg>