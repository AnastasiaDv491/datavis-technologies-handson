<script>
    import * as d3 from "d3";
    import { onMount } from 'svelte';
    // import Scatterplot from "./Scatterplot.svelte";

 
    let data = [];
    onMount(async () => {
        console.log("onMount started!");
        data = await d3.csv("/data/cars-2.csv");

        console.log("Data loaded!");
    });

    console.log("Script finished!")
</script>

{#each data as post}
    <h3>{post.Name}</h3>
{/each}