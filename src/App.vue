<template>
  <div id="app">
    <Main class="main" />
  </div>
</template>

<script>
export default {
  name: "App",
  components: {
    Main: () => import("@/components/main/Index")
  }
};
</script>

<style lang="scss" scoped>
.main {
  position: absolute;
  width: 100vw;
  height: auto;
  min-height: 100vh;
  text-align: center;
  z-index: 1;
  border-radius: 10px;
}

.box {
  width: 50%;
  height: 50%;
  position: absolute;
  text-align: center;

  &.pos1 {
    top: 0%;
    left: 0%;
  }

  &.pos2 {
    top: 0%;
    left: 50%;
  }

  &.pos3 {
    top: 50%;
    left: 0%;
  }

  &.pos4 {
    top: 50%;
    left: 50%;
  }
}
</style>
