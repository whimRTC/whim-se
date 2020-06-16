<template>
  <div>
    <template v-if="isMe">
      <a class="fuwatto_btn" @click="cheer"><img src="@/assets/claps.png"/></a>
      <a class="fuwatto_btn" @click="cracker"
        ><img src="@/assets/cracker.svg"
      /></a>
      <a class="fuwatto_btn" @click="correct">正解</a>
      <a class="fuwatto_btn" @click="incorrect">
        <img src="@/assets/cross.svg" class="cross"
      /></a>
    </template>
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
    },
    isMe() {
      return this.$whim.accessUser.id === this.displayUser.id;
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
      this.sendSound("cracker1.mp3");
    },
    correct() {
      this.sendSound("correct1.mp3");
    },
    incorrect() {
      this.sendSound("incorrect1.mp3");
    }
  },
  watch: {
    sound: function(newSound) {
      this.play(newSound);
    }
  }
};
</script>
<style lang="scss" scoped>
.fuwatto_btn {
  display: block;
  background-color: #67c5ff;
  color: #fff;
  margin: 10px;
  padding: 0.8em;
  text-decoration: none;
  border-radius: 50px;
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.12), 0 1px 5px 0 rgba(0, 0, 0, 0.12),
    0 3px 1px -2px rgba(0, 0, 0, 0.2);
  transition: 0.3s ease-out;
  width: 50px;
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
.cross {
  width: 70%;
}
</style>
