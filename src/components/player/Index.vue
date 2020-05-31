<template>
  <div>
    <button @click="cheer">歓声</button>
    <button @click="cracker">クラッカー</button>
    <button @click="correct">正解</button>
    <button @click="incorrect">不正解</button>
  </div>
</template>
<script>
import { Howl } from "howler";
export default {
  name: "Player",
  props: {
    displayUser: {
      // 表示されているUserの情報
      type: Object,
      required: true
    }
  },
  methods: {
    play(src) {
      const sound = new Howl({
        src: src
      });
      sound.volume(1.0);
      if (sound.playing()) {
        sound.stop();
      } else {
        sound.play();
      }
    },
    cheer() {
      this.play(require("@/assets/people-performance-cheer1.mp3"));
    },
    cracker() {
      this.play(require("@/assets/cracker1.mp3"));
    },
    correct() {
      this.play(require("@/assets/correct1.mp3"));
    },
    incorrect() {
      this.play(require("@/assets/incorrect1.mp3"));
    }
  }
};
</script>
<style lang="scss" scoped></style>
