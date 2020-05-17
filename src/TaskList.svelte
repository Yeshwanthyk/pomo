<script>
  import { afterUpdate } from "svelte";
  import { Task } from "./Task.js";

  let tasks = [
    new Task("Slingshot"),
    new Task("Riverbeast"),
    new Task("Manchvegas")
  ];
</script>

<style>
  ul {
    list-style: none;
  }
  .description {
    min-width: 400px;
  }
  .pomodoro {
    max-width: 100px;
  }
</style>

<ul>
  {#each tasks as task}
    <li>
      <input class="description" type="text" bind:value={task.description} />
      <input
        class="pomodoro"
        type="number"
        bind:value={task.expectedPomodoros} />
    </li>
  {/each}
</ul>
