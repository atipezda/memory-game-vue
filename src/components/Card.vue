<template>
  <div :style="{ backgroundColor: color }" class="card">
    <div class="card-face is-front">
      <div class="matched"></div>
    </div>
    <div class="card-face is-back"></div>
  </div>
</template>

<script>
export default {
  props: {
    color: {
      type: String,
      required: true,
    },
  },
};
</script>

<style>
.card {
  border: 1px solid #fff;
  border-radius: 10px;
  cursor: pointer;
}
.card-face.is-front {
  position: absolute;
}
.is-back {
  height: 100%;
}
</style>
