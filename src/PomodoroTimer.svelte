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

  function formatTime(timeInSeconds) {
    const minutes = secondsToMinutes(timeInSeconds);
    const remainingSeconds = timeInSeconds % 60;
    return `${padWithZeroes(minutes)}:${padWithZeroes(remainingSeconds)}`;
  }

  let interval;
  function startPomo() {
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
    pomodoroTime = time;
    interval = setInterval(() => {
      if (pomodoroTime === 0) {
        idle();
      }
      pomodoroTime -= 1;
    }, 1000);
  }

  function idle() {
    clearInterval(interval);
    pomodoroTime = POMODORO_S;
  }

  function cancelPomo() {
    // TODO: Add some logic to prompt user to write down
    //   cause of interruption
    idle();
  }
</script>

<section>
  <p>{formatTime(pomodoroTime)}</p>
  <button on:click={startPomo}>start</button>
  <button on:click={cancelPomo}>cancel</button>
</section>
