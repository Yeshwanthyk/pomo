<script>
  const minutesToSeconds = minutes => minutes * 60;
  const secondsToMinutes = seconds => Math.floor(seconds / 60);
  const padWithZeroes = number => number.toString().padStart(2, "0");

  const LONG_BREAK_S = minutesToSeconds(20);
  const SHORT_BREAK_S = minutesToSeconds(5);
  let completedPomodoros = 0;

  // length of the pomodoro in seconds
  const POMODORO_S = minutesToSeconds(25);

  // Pomodoro time left
  let pomodoroTime = POMODORO_S;

  const State = { idle: "idle", inProgress: "in progress", resting: "resting" };
  let currentState = State.idle;

  function formatTime(timeInSeconds) {
    const minutes = secondsToMinutes(timeInSeconds);
    const remainingSeconds = timeInSeconds % 60;
    return `${padWithZeroes(minutes)}:${padWithZeroes(remainingSeconds)}`;
  }

  let interval;

  function startPomo() {
    currentState = State.inProgress;
    interval = setInterval(() => {
      if (pomodoroTime === 0) {
        completePomodoro();
      }

      pomodoroTime -= 1;
    }, 1000);
  }

  function completePomodoro() {
    clearInterval(interval);
    completedPomodoros++;

    completedPomodoros++;
    if (completedPomodoros === 4) {
      rest(LONG_BREAK_S);
    } else {
      rest(SHORT_BREAK_S);
    }
  }

  function rest(time) {
    currentState = State.resting;
    pomodoroTime = time;
    interval = setInterval(() => {
      if (pomodoroTime === 0) {
        idle();
      }
      pomodoroTime -= 1;
    }, 1000);
  }

  function idle() {
    currentState = State.idle;
    clearInterval(interval);
    pomodoroTime = POMODORO_S;
  }

  function cancelPomo() {
    // TODO: Add some logic to prompt user to write down
    //   cause of interruption
    idle();
  }
</script>

<style>
  time {
    display: block;
    font-size: 5em;
    font-weight: 300;
    margin-bottom: 0.2em;
  }
</style>

<section>
  <time>{formatTime(pomodoroTime)}</time>
  <button on:click={startPomo} disabled={currentState !== State.idle}>
    start
  </button>
  <button on:click={cancelPomo} disabled={currentState !== State.inProgress}>
    cancel
  </button>
</section>
