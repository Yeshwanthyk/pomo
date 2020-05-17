<script>
  const tasks = ["One world", "One ring", "Slingshot cops"];
</script>

<ul>
  {#each tasks as task}
    <li>{task}</li>
  {/each}
</ul>
