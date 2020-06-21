<template>
  <div>
    <template>
      <a class="fuwatto_btn" @click="cheer"><img src="@/assets/claps.png"/></a>
      <a
        class="fuwatto_btn"
        @click="drumroll"
        :class="{ active: sound === 'drum' }"
      >
        <img src="@/assets/drum.svg"
      /></a>
      <a class="fuwatto_btn" @click="sendSound('chanchan')">
        <img src="@/assets/trumpet.svg" class="trumpet"
      /></a>
      <a class="fuwatto_btn" @click="sendSound('tin')">
        <img src="@/assets/tin.svg"
      /></a>
      <a class="fuwatto_btn" @click="sendSound('spring')">
        <img src="@/assets/clown.svg"
      /></a>
      <a class="fuwatto_btn" @click="sendSound('shine')">
        <img src="@/assets/diamond.svg"
      /></a>
      <a class="fuwatto_btn" @click="sendSound('bomb')">
        <img src="@/assets/bomb.svg"
      /></a>
      <a class="fuwatto_btn" @click="correct"
        ><img src="@/assets/circle.png"
      /></a>
      <a class="fuwatto_btn" @click="incorrect">
        <img src="@/assets/cross.svg"
      /></a>
      <a class="fuwatto_btn" @click="sendSound('wolf')">
        <img src="@/assets/wolf.svg"
      /></a>
      <!-- <a class="fuwatto_btn" @click="cracker"
        ><img src="@/assets/cracker.svg"
      /></a> -->
    </template>
  </div>
</template>
<script>
import { Howl } from "howler";

const SE = {
  cheer: new Howl({ src: require("@/assets/people-performance-cheer1.mp3") }),
  cracker: new Howl({ src: require("@/assets/cracker1.mp3") }),
  correct: new Howl({ src: require("@/assets/correct1.mp3") }),
  incorrect: new Howl({ src: require("@/assets/incorrect1.mp3") }),
  drum: new Howl({ src: require("@/assets/drum-roll1.mp3") }),
  rollFinish: new Howl({ src: require("@/assets/roll-finish1.mp3") }),
  chanchan: new Howl({ src: require("@/assets/chan-chan2.mp3") }),
  tin: new Howl({ src: require("@/assets/tin1.mp3") }),
  shine: new Howl({ src: require("@/assets/shine4.mp3") }),
  spring: new Howl({ src: require("@/assets/boyoyon1.mp3") }),
  bomb: new Howl({ src: require("@/assets/bomb1.mp3") }),
  wolf: new Howl({ src: require("@/assets/wolf.wav") })
};
export default {
  name: "Main",
  computed: {
    sound() {
      return this.$whim.state.sound;
    }
  },
  methods: {
    play(src) {
      const sound = SE[src];
      sound.volume(0.15);
      sound.play();
      setTimeout(
        () => {
          this.$whim.assignState({
            sound: null
          });
        },
        src === "drum" ? 4000 : 0
      );
    },
    sendSound(src) {
      this.$whim.assignState({
        sound: src
      });
    },
    cheer() {
      this.sendSound("cheer");
    },
    cracker() {
      this.sendSound("cracker");
    },
    correct() {
      this.sendSound("correct");
    },
    incorrect() {
      this.sendSound("incorrect");
    },
    drumroll() {
      if (this.sound === "drum") {
        this.sendSound("rollFinish");
      } else {
        this.sendSound("drum");
      }
    }
  },
  watch: {
    sound: function(newSound) {
      if (newSound === "rollFinish") {
        SE.drum.stop();
      }
      if (newSound) this.play(newSound);
    }
  }
};
</script>
<style lang="scss" scoped>
.fuwatto_btn {
  display: block;
  background-color: #ffe605;
  margin: 1vh;
  padding: 1vh;
  text-decoration: none;
  border-radius: 5vh;
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.12), 0 1px 5px 0 rgba(0, 0, 0, 0.12),
    0 3px 1px -2px rgba(0, 0, 0, 0.2);
  transition: 0.3s ease-out;
  width: 5vh;
  text-align: center; /*一応BOX内の文字も中央寄せ*/
  &:hover {
    cursor: pointer;
    text-decoration: none;
    box-shadow: 0 5px 10px 0 rgba(0, 0, 0, 0.12),
      0 3px 20px 0 rgba(0, 0, 0, 0.12), 0 5px 6px -2px rgba(0, 0, 0, 0.2);
  }
}
img {
  width: 100%;
}
// .cross {
//   width: 70%;
// }
.trumpet {
  transform: rotate(-30deg);
}
.active {
  background-color: #ff0505;
}
</style>
