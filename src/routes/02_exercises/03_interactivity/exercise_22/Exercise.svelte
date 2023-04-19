<script>
    let i = 0;
    function myCallback() {
        i +=1;
    }

    function myReset(){
        i = 0
    }
</script>

<button type="button" class="btn btn-primary" on:click={myCallback}>Click</button>

<button type="button" class="btn btn-primary" on:click={myReset}>Reset</button>
<p>you have clicked the button {i} times</p>
