<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  // Properties
  export let data = [];
  const continents = ["europe", "asia", "americas", "africa"];
  export let selected_continent;
  export let slider_value = 0;                                              
    
</script> 

<div class="column">
  <input type="range" min="0" max="214" bind:value={slider_value} /><br/>
  <p>Year: {data[slider_value].year}</p>


  <button type="button" class="btn btn-primary">Reset</button>
  <button type="button" class="btn btn-success">Play Pause</button>
  <select name="language" id="language" bind:value = {selected_continent} >
    {#each continents as continent}
    <option value={continent}>{continent}</option>

    {/each}
  </select>
  

</div>
