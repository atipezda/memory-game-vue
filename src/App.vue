<template>
  <Card v-for="(card, index) in cardList" :key="index" :color="card.color" />
</template>

<script>
import Card from "./components/Card";
import { ref } from "vue";

export default {
  name: "App",
  components: {
    Card,
  },
  setup() {
    const cardList = ref([]);

    const cardItems = [
      "#6600FF",
      "#990033",
      "#FFFF00",
      "#0E0E0E",
      "#76FF03",
      "#00FF00",
      "#696969",
      "#CF7E3C",
    ];
    cardItems.forEach((item) => {
      cardList.value.push({
        color: item,
      });

      cardList.value.push({
        color: item,
      });
    });
    cardList.value = cardList.value.map((card, index) => {
      return {
        ...card,
        position: index,
      };
    });

    return {
      cardList,
    };
  },
};
</script>

<style></style>
