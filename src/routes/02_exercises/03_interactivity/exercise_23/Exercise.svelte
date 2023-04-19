<script>
    // Dimensions
    const width = 800;
    const height = 100;
    const margin = { top: 10, right: 20, bottom: 20, left: 20 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
  
    // Arrays
    const points = [
      innerWidth / 2 - 60,
      innerWidth / 2 - 30,
      innerWidth / 2,
      innerWidth / 2 + 30,
      innerWidth / 2 + 60
    ];
  
    // All lights with a higher index are on!
    let index = points.length;
    let color;
    // const incr = () => (index -= 1)
    function decreaseInt(){
      index -=1
      if (index <= -1){
        clearInterval(clear)
        color = "darkgreen"
      }
    }
    let clear
    $: {
      clear = setInterval(decreaseInt,1000)
      color = "darkred";
      console.log(clear)
    }
    
    // index = -1;
    // TODO: 
    // Color

  </script>
  
  <svg viewBox="0 0 {width} {height}">
    <g transform="translate({margin.left},{margin.top})">
      {#each points as position, i}
      {#if i >= index}
      <circle r = 10 cx = {position} class = "circle_light"  fill= {color} opacity = 1/>
      {:else}
      <circle r = 10 cx = {position} class = "circle_light"  fill= {color} opacity = 0.3/>

      {/if}
      {/each}
    </g>
  </svg>

  <p>{index}</p>
  <style>
    
  </style>
  