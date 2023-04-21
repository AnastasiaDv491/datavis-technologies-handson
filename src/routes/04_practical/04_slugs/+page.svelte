<script>
    export let data;
    $: console.log(data)
</script>

<ul>
    {#each data.flowers as flower}
    <li>{flower.id}</li>
    {/each}
</ul>