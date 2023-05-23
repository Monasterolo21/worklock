<template>
  <div>
    <div class="round-corner">
      <div class="timer" :class="{ paused: !timerActive }">
        {{ formattedTime }}
      </div>
    </div>

    <div class="set-section">
      <h2>SET DONE</h2>
      <div class="set-container">
        <button class="action-button" @click="decrementCounter">
          <span class="material-symbols-rounded"> remove </span>
        </button>
        <span class="counter">{{ counter }}</span>
        <button class="action-button" @click="incrementCounter">
          <span class="material-symbols-rounded"> add </span>
        </button>
      </div>
    </div>

    <div class="action-section">
      <button @click="toggleTimer">
        <span class="material-symbols-rounded"> play_pause </span>
      </button>
      <button @click="reset">
        <span class="material-symbols-rounded"> device_reset </span>
      </button>
      <button @click="cheer">
        <span class="material-symbols-rounded">
          <img src="../assets/logo.png" alt="cheer" width="25" height="25" />
        </span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      counter: 0,
      timer: 0,
      timerActive: false,
      intervalId: null,
    };
  },
  computed: {
    formattedTime() {
      const minutes = Math.floor(this.timer / 60);
      const remainingSeconds = this.timer % 60;
      const minutesDisplay = minutes < 10 ? "0" + minutes : minutes;
      const secondsDisplay =
        remainingSeconds < 10 ? "0" + remainingSeconds : remainingSeconds;
      return `${minutesDisplay}:${secondsDisplay}`;
    },
  },
  methods: {
    incrementCounter() {
      this.counter++;
      this.disableResetButton = false;
      this.disableTimerButton = false;
      this.reset();
      this.toggleTimer();
    },
    decrementCounter() {
      if (this.counter > 0) {
        this.counter--;
      }
      if (this.counter === 0) {
        this.disableResetButton = true;
        this.disableTimerButton = true;
      }
      this.reset();
      this.toggleTimer();
    },
    reset() {
      this.timerActive = false;
      clearInterval(this.intervalId);
      this.timer = 0;
    },
    cheer() {
      // alert("Dai uomo!");
      // reproduce sound
      const audio = new Audio(require("../assets/audio/vaiUomo.mp3"));
      audio.play();
    },

    toggleTimer() {
      if (this.timerActive) {
        this.stopTimer();
      } else {
        this.startTimer();
      }
    },
    startTimer() {
      if (!this.timerActive) {
        this.timerActive = true;
        this.intervalId = setInterval(() => {
          this.timer++;
        }, 1000);
      }
    },

    stopTimer() {
      if (this.timerActive) {
        this.timerActive = false;
        clearInterval(this.intervalId);
      }
    },
  },
};
</script>

<style>
.round-corner {
  border-radius: 100%;
  background-color: transparent;
  color: var(--secondary-color);
  padding: 1em;
  display: flex;
  justify-content: center;
  align-items: center;
  display: flex;
  align-items: center;
  border: 2px solid var(--secondary-color);
  /* make same height that width */
  width: 10em;
  height: 10em;
}

.set-section {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 4em 1em 1em;
  /* align content vertically */
  flex-direction: column;
  padding: 0;
}

.set-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0em 0;
  flex-direction: row;
  padding: 0;
}

.set-section h2 {
  margin: 0;
  font-size: 1.6em;
  color: var(--primary-color);
  display: block;
  width: 100%;
  padding: 0;
  padding-bottom: -2em;
  font-weight: 500;
}

.timer {
  font-size: 3em;
  color: var(--text-color);
}

.paused {
  opacity: 0.5;
}

.counter {
  display: flex;
  align-items: center;
  font-size: 3em;
  vertical-align: middle;
  padding-bottom: 0.2em;
  color: var(--text-color);
}

.action-button {
  background-color: transparent;
  border: 1px solid var(--primary-color);
  border-radius: 50%;
  width: auto;
  height: auto;
  margin: 0 15px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  color: var(--primary-color);
  padding: 0.15em;
  font-size: 2em;
  vertical-align: top;
}

button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

button {
  background-color: transparent;
  border: 1px solid var(--primary-color);
  border-radius: 100%;
  width: auto;
  height: auto;
  margin: 0 15px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  color: var(--primary-color);
  padding: 0.2em;
  font-size: 1.6em;
  margin: 0.3em;
  vertical-align: top;
}

.action-section {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 1em 1em;
  /* align content vertically */
  flex-direction: row;
  padding: 0;
}
</style>
