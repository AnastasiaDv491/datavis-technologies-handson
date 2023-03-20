<script>
	let clicked = false;
</script>

<div>
	
	<button class="btn btn-primary" on:click={() => (clicked = true)}>
		click here
	</button>
	{#if clicked = false}
		<p>h</p>
	{:else}
		<p>hhh</p>
	{/if}
	<!-- {#if clicked = true}
		<p>You clicked!</p>
	{:else}
	<p>You didnt</p>
	{/if} -->

</div>
