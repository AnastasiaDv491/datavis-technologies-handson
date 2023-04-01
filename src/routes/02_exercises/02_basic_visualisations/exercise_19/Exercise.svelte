<script>
    import { scaleLinear} from 'd3-scale';
    import { tick } from 'svelte';
    import * as d3 from "d3"


    // Dimensions
    const width = 1000;
    const height = 1000;
    const margin = { top: 20, right: 5, bottom: 5, left: 5 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
  
    // Array
    const values = [
      { x: 2, y: 1, category: "cat1" },
      { x: 4, y: 2, category: "cat3" },
      { x: 6, y: 1, category: "cat2" },
      { x: 7, y: 3, category: "cat3" },
      { x: 9, y: 1, category: "cat2" }
    ];

    for (let i in values){
      for (let j in values[i])
        console.log(j)
    }
      
    var accent = d3.scaleOrdinal(d3.schemeDark2);


    let xScale = scaleLinear()
      .domain([0,15])
      .range([0, innerWidth])
    let yScale = scaleLinear()
      .domain([0,15])
      .range([innerHeight,0])
    
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
  
  <svg viewBox="0 0 {width} {height}">
    <g transform="translate(20,{innerHeight})">
      <g class="x-axis" bind:this={xAxis}></g>
    </g>
    
    <g transform="translate(20, 0)">
      <g class="y-axis" bind:this={yAxis}></g>

    </g> 
    <g>
      {#each values as value}
      <text x = {xScale(value.x)} y = {yScale(value.y)-10}>{value.y}</text>
      <circle cx = {xScale(value.x)} cy = {yScale(value.y)} r = 10 fill= {accent(value.category)}/>
      
      <line x1 = {xScale(value.x)} y1 = {yScale(value.y)} x2 = {xScale(value.x)} y2 = {innerHeight} stroke="black"></line>
      {/each}
   
    </g>
  </svg>
  
  <style>
    text {
      text-anchor: middle;
      font-size: xx-large;
    }
   
  </style>
  