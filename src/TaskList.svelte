<script>
  import { afterUpdate } from "svelte";
  import { Task } from "./Task.js";

  let taskAddedFocusPending = true;
  let lastInput;

  let tasks = [
    new Task("Slingshot"),
    new Task("Riverbeast"),
    new Task("Manchvegas")
  ];

  $: allExpectedTasks = tasks.reduce((acc, t) => acc + t.actualPomodoros, 0);

  function addTask() {
    //   tasks.push won't work because svelte works with change in
    //   assignment
    tasks = tasks.concat(new Task());
    taskAddedFocusPending = true;
  }

  function removeTask(task) {
    const index = tasks.indexOf(task);
    tasks = [...tasks.slice(0, index), ...tasks.slice(index + 1)];
  }

  function focusNewTask() {
    if (taskAddedFocusPending && lastInput) {
      lastInput.focus();
      taskAddedFocusPending = false;
    }
  }

  afterUpdate(focusNewTask);
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

{#if tasks.length === 0}
  <p>Add a task. You can do it!</p>
{:else}
  <ul>
    {#each tasks as task}
      <li>
        <input
          class="description"
          type="text"
          bind:value={task.description}
          bind:this={lastInput} />
        <input
          class="pomodoro"
          type="number"
          bind:value={task.expectedPomodoros} />
      </li>
      <button on:click={() => removeTask(task)}>X</button>
    {/each}
  </ul>
{/if}
<button on:click={addTask}>Add a new task</button>

{#if tasks.length !== 0}
  <p>Today you'll complete {allExpectedTasks} pomodoros.</p>
{/if}
