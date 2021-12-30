<template>
  <div class="card">
    <div class="card-face is-front">
      <div class="matched">{{color}}</div>
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
    }
  }
}
</script>

<style></style>
