<script>
  import { extent } from "d3-array";
  import { select } from "d3-selection";
  import { scaleLinear } from "d3-scale";
  import { axisBottom, axisLeft } from "d3-axis";
  import { brush } from "d3-brush";
    import { color } from "d3";

  // Properties
  export let data = [];
  export let x = (d) => d.x;
  export let y = (d) => d.y;
  export let xLabel = "x";
  export let yLabel = "y";

  //Own properties
  export let pointsSelectedInBoth;
  export let pointsSelected = [];
  let coords = [];

  // Dimensions
  const width = 300;
  const height = 230;
  const margin = { top: 10, right: 10, bottom: 35, left: 45 };
  const innerWidth = width - margin.left - margin.right;
  const innerHeight = height - margin.top - margin.bottom;

  // Scales
  const xScale = scaleLinear().domain(extent(data, x)).range([0, innerWidth]);
  const yScale = scaleLinear().domain(extent(data, y)).range([innerHeight, 0]);

  // Axes
  const xAxis = (node) => axisBottom(xScale)(select(node));
  const yAxis = (node) => axisLeft(yScale)(select(node));

  // Brushing
  // The range of the selection rectangle.
  // If there is no active selection, it contains: null,
  // otherwise, it contains: [ [x0, y0], [x1, y1] ]
  let range = null;

  // brush()
  // .on('start', doStart)
  // .on('brush', doMove)
  // .on('end', doEnd)
  function brushActivation(node) {
    // console.log(node);
    select(node).call(
      brush().on("start", doStart).on("brush", doMove).on("end", doEnd)
    );
  }
  function doStart({ selection }) {
    // console.log({ selection });
    range = selection;
  }

  function doMove({ selection }) {
    // console.log({ selection });
    range = selection;
  }

  function doEnd({ selection }) {
    // console.log({ selection });
    range = selection;
  }

  data.forEach((element) => {
    let xpoint = xScale(x(element));
    let ypoint = yScale(y(element));
    coords.push({xpoint, ypoint});
  });

  function handleRangeChange(){
    console.log("changed range");
    if (range) {
      for (let index = 0; index < coords.length; index++) {
        const element = coords[index];
        // console.log(element)
        if(range[0][0] <= element.xpoint && element.xpoint <= range[1][0] &&  range[0][1] <= element.ypoint &&element.ypoint <= range[1][1]){
          pointsSelected[index] = true
        }
        else {
          pointsSelected[index] = false
        }
      }
    }
    else{
      // Range is null
      console.log("range is null");
      pointsSelected = [];
      for (let i = 0; i < coords.length; i++) {
        pointsSelected[i] = true;
      }
    }
  }

  $: range, handleRangeChange();


  // function changeCSSAttributes(){
  //   for (let index = 0; index < pointsSelectedInBoth.length; index++) {
  //     if (pointsSelectedInBoth[index] = false){
  //       opacity = "0.3"
  //       stroke_opacity = "0.5"
  //       fill = "darkgray"
  //     }
  //     else{
  //       opacity = "1"
  //       stroke_opacity = "1"
  //       fill = "steelblue"
  //     }
  //   }
  // }
  $: pointsSelected
  
</script>

<svg viewBox="0 0 {width} {height}" class="mx-2" style="max-width: {width}px">
  <g transform="translate({margin.left},{margin.top})">
    <g id="groupForBrush" use:brushActivation>
      {console.log(pointsSelectedInBoth)}

      {#each coords as d, i}
        {#if pointsSelectedInBoth[i] == true}
        <!-- svelte-ignore a11y-mouse-events-have-key-events -->
        <circle
          cx={d.xpoint}
          cy={d.ypoint}
          r={2}
          fill="steelblue"
          fill-opacity="0.5"
          stroke='steelblue'
          stroke-width="1.5"
          stroke-opacity= "1"
          opacity = "1"
        />
        {:else}
          <circle
          cx={d.xpoint}
          cy={d.ypoint}
          r={2}
          fill="darkgrey"
          fill-opacity="0.3"
          stroke='darkgrey'
          stroke-width="1.5"
          stroke-opacity= "0.5"
          opacity = "1"
        />
        {/if}
      {/each}
    </g>
    <g use:xAxis transform="translate(0, {innerHeight})">
      <text class="axisLabel" x={innerWidth / 2} y={margin.bottom - 5}
        >{xLabel}</text
      >
    </g>
    <g use:yAxis>
      <text
        class="axisLabel"
        y={-margin.left + 10}
        x={-innerHeight / 2}
        transform="rotate(-90)">{yLabel}</text
      >
    </g>
  </g>
</svg>

<style>
  .axisLabel {
    text-anchor: middle;
    vertical-align: bottom;
    fill: currentcolor;
  }

</style>
