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
  computed: {
    sound() {
      return this.$whim.state.sound;
    }
  },
  methods: {
    play(src) {
      const sound = new Howl({
        src: require(`@/assets/${src}`)
      });
      sound.volume(0.8);
      sound.play();
    },
    sendSound(src) {
      this.$whim.assignState({
        sound: src
      });
    },
    cheer() {
      this.sendSound("people-performance-cheer1.mp3");
    },
    cracker() {
      this.sendSound("@/assets/cracker1.mp3");
    },
    correct() {
      this.sendSound("@/assets/correct1.mp3");
    },
    incorrect() {
      this.sendSound("@/assets/incorrect1.mp3");
    }
  },
  watch: {
    sound: function(newSound) {
      this.play(newSound);
    }
  }
};
</script>
<style lang="scss" scoped></style>
