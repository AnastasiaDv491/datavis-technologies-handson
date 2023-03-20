<script>
  let current = "";
</script>

<!-- We will cover buttons later on! -->
<button class="btn btn-secondary" on:click={() => (current = "messi")} class:active = {current =="messi"}>
  Messi
</button>

<button class="btn btn-secondary" on:click={() => (current = "ronaldo")} class:active = {current == "ronaldo"}>
  Ronaldo
</button>

<button class="btn btn-secondary" on:click={() => (current = "neymar")} class:active = {current == "neymar"}>
  Neymar
</button>

<style>
  .active{
    background-color: antiquewhite;
  }
</style>