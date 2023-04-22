<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  // Properties
  export let data = [];
  const continents = ["all","europe", "asia", "americas", "africa"];
  export let selected_continent;
  export let slider_value = 0;                                              
    
  // const incr = () => (index -= 1)
  function decreaseInt(){
    slider_value +=1
    if (slider_value >=2014){
      clearInterval(clear)
    }
  }
  let clear
  function setInt(){
    clear = setInterval(decreaseInt,500)
  }

  function resetInt(){
    slider_value = 0;
    clear = setInterval(decreaseInt,500)
  }

</script> 

<div class="column">
  <input type="range" min="0" max="214" bind:value={slider_value} /><br/>
  <p>Year: {data[slider_value].year}</p>


  <button type="button" class="btn btn-primary" on:click={resetInt}>Reset</button>
  <button type="button" class="btn btn-success" on:click={setInt}>Play Pause</button>
  <select name="language" id="language" bind:value = {selected_continent} >
    {#each continents as continent}
    <option value={continent}>{continent}</option>

    {/each}
  </select>
  

</div>
