<script>
const student =  {name: 'Nastya', things:['cooking', 'running', 'playing']}

</script>

My name is {student.name} and these are my fav things: 
{#each student.things as thing}
<li>
    {thing}
</li>
{/each}