<script>
    import * as d3 from "d3";
    import { onMount } from 'svelte';
    import Scatterplot from "./Scatterplot.svelte";

 
    let data;
    onMount(async () => {
        console.log("onMount started!");
        
        data = await d3.json("/data/gapminder.json");

        //Get max income
        console.log(Math.max(...data[0].countries.map(o => o.income)));
        //Get max life expectancy
        console.log(Math.max(...data[0].countries.map(o => o.population)));
        

        console.log(data[0].countries)
        console.log("Data loaded!");
    });

    console.log("Script finished!")
</script>

<Scatterplot dataExcercise={data}></Scatterplot>