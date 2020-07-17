<template>
  <div id="app">
    <div class="game-container">
      <!--Enemy-->
      <div id="enemy">
        <img
          src="./assets/01.png"
          alt="Enemy logo"
          id="challenge"
          v-bind:style="{ display: challenge }"
        />
        <img
          src="./assets/02.png"
          alt="Enemy logo"
          id="lose"
          v-bind:style="{ display: show }"
        />
      </div>
      <!--Enemy Health-->

      <span v-bind:style="{ width: health + 'px' }"></span>
      <div id="enemy-health"></div>

      <!--Controls-->
      <div id="controls">
        <img
          src="./assets/03.png"
          alt="Punch Button"
          v-show="!ended"
          v-on:click="punch"
        />
        <button v-on:click="restart">Restart</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      health: 250,
      ended: false,
      show: "none",
      challenge: "block"
    };
  },
  methods: {
    punch: function() {
      this.health -= 10;
      if (this.health <= 0) {
        this.ended = true;
        this.show = "block";
        this.challenge = "none";
      }
    },
    restart: function() {
      this.health = 250;
      this.challenge = "block";
      this.show = "none";
      this.ended = false;
    }
  }
};
</script>

<style lang="scss">
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body,
html {
  font-family: sans-serif;
}

.game-container {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background: url(./assets/bg.gif) no-repeat;
  background-size: cover;
  background-position: center;
}

#enemy #challenge {
  width: 250px;
  position: relative;
  left: -20px;
}

#enemy #lose {
  display: none;
}
#enemy-health {
  height: 30px;
  padding: 14px;
  width: 250px;
  border: 2px #110303 solid;
  background: rgb(156, 112, 108);
  animation: animate 1s linear infinite;
}

@keyframes animate {
  from {
    box-shadow: #110303 0 0 10px;
  }
  to {
    box-shadow: #eed9d9 0 0 10px;
  }
}
span {
  height: 30px;
  width: 250px;
  background: rgb(7, 223, 43);
  z-index: 1;
  position: relative;
  top: 31px;
}

#controls {
  display: flex;
  flex-direction: column;
}
#controls img {
  width: 100px;
  cursor: pointer;
  margin-top: 30px;
}

#controls img:active {
  transform: scale(1.2);
}

#controls button {
  padding: 12px;
  width: 120px;
  background: rgb(255, 255, 255);
  border: none;
  margin-top: 40px;
  cursor: pointer;
}

#controls button:hover {
  background: #ffc400;
  transition: 0.3s;
}

@media screen and (max-width: 720px) {
  #enemy #lose {
    width: 270px;
  }
}
</style>
