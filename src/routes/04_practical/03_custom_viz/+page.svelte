<script>
    import Papa from 'papaparse';
    import Flower from './Flower.svelte';

    let datapoints = []

    Papa.parse("https://vda-lab.github.io/assets/iris.csv", {
        header: true,
        download: true,
        complete: function(results) {
            datapoints = results.data
        }
    })

    const get_xy = function(idx) {                                     
        let y = 25 + (Math.floor(idx / 20) * 50)
        let x = 25 + ((idx % 20) * 50)
        return [x,y]
    }
    $: console.log(datapoints)                                         
</script>

<svg width=1000 height=1000>
    {#each datapoints as datapoint,idx}                                
        <g transform="translate({get_xy(idx)[0]}, {get_xy(idx)[1]})">  
            <Flower datapoint={datapoint} />
        </g>
    {/each}
</svg>