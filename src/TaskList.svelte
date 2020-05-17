<script>
  import { afterUpdate } from "svelte";
  import { Task } from "./Task.js";

  let tasks = [
    new Task("Slingshot"),
    new Task("Riverbeast"),
    new Task("Manchvegas")
  ];

  function addTask() {
    //   tasks.push won't work because svelte works with change in
    //   assignment
    tasks = tasks.concat(new Task());
  }

  function removeTask(task) {
    const index = tasks.indexOf(task);
    tasks = [...tasks.slice(0, index), ...tasks.slice(index + 1)];
  }
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
    <button on:click={() => removeTask(task)}>X</button>
  {/each}
</ul>
<button on:click={addTask}>Add a new task</button>
