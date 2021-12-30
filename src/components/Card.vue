<template>
  <div class="card">
    <div :style="{ backgroundColor: value }" class="card-face is-front">
      <div v-if="matched" class="matched">siema</div>
    </div>
    <div class="card-face is-back">LOLS</div>
  </div>
</template>

<script>
export default {
  props: {
    color: {
      type: String,
      required: true,
    },
    matched: {
      type: Boolean,
      default: true,
    },
    visible: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style>
.card {
  border: 1px solid #fff;
  border-radius: 10px;
  position: relative;
  cursor: pointer;
}
.card-face.is-front {
  position: absolute;
  width: 100%;
  height: 100%;
}
.is-back {
  background-color: white;

  height: 100%;
}
.matched {
  position: absolute;
  background-color: white;
  transform: 1s;
  opacity: 0.3;
  width: 100%;
  height: 100%;
}
</style>
