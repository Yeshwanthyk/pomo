<script>
  export let title = "Pomo";
  import TaskList from "./TaskList.svelte";
  import PomodoroTimer from "./PomodoroTimer.svelte";
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 6em;
    margin: 0;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main>
  <h1>{title}!</h1>
  <PomodoroTimer />
  <TaskList />
</main>
