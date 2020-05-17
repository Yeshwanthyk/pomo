<script>
  const minutesToSeconds = minutes => minutes * 60;
  const secondsToMinutes = seconds => Math.floor(seconds / 60);
  const padWithZeroes = number => number.toString().padStart(2, "0");

  // length of the pomodoro in seconds
  const POMODORO_S = minutesToSeconds(25);

  // Pomodoro time left
  let pomodoroTime = POMODORO_S;

  function formatTime(timeInSeconds) {
    const minutes = secondsToMinutes(timeInSeconds);
    const remainingSeconds = timeInSeconds % 60;
    return `${padWithZeroes(minutes)}:${padWithZeroes(remainingSeconds)}`;
  }

  function startPomo() {
    setInterval(() => {
      pomodoroTime -= 1;
    }, 1000);
  }
</script>

<section>
  <p>{formatTime(pomodoroTime)}</p>
  <button on:click={startPomo}>start</button>
</section>
