<template>
  <h1>MEMORY GAMME</h1>
  <section class="gameBoard">
    <Card
      v-for="(card, index) in cardList"
      :key="index"
      :color="card.color"
      :visible="card.visible"
      :matched="card.matched"
    />
  </section>
  <h2>{{ status }}</h2>
  <button class="ressButton">Reset Gry</button>
</template>

<script>
import Card from "./components/Card";
import { computed, ref } from "vue";

export default {
  name: "App",
  components: {
    Card,
  },
  setup() {
    const cardList = ref([]);

    const status = computed(() => {
      if (remainingPairs.value === 0) {
        return "Gracz Wygrywa";
      } else {
        return `Pozostałe Pary: ${remainingPairs.value}`;
      }
    });

    const remainingPairs = computed(() => {
      const remainingCards = cardList.value.filter(
        (card) => card.matched === false
      ).length;
      return remainingCards / 2;
    });

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
        visible: false,
        matched: false,
      });

      cardList.value.push({
        color: item,
        visible: false,
        matched: false,
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
      status,
    };
  },
};
</script>

<style>
body {
  background-color: #1b1e20;
}
h1,
h2 {
  text-align: center;
  color: #fff;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  position: relative;
}
.gameBoard {
  display: grid;
  grid-template-columns: repeat(4, 150px);
  grid-template-rows: repeat(4, 150px);
  grid-column-gap: 5vw;
  grid-row-gap: 4vh;
  justify-content: center;
}
.ressButton {
  box-shadow: inset 0px 1px 3px 0px #91b8b3;
  background: linear-gradient(to bottom, #e8e8e8 5%, #6c7c7c 100%);
  background-color: #e8e8e8;
  border-radius: 5px;
  border: 1px solid #566963;
  display: inline-block;
  cursor: pointer;
  color: #ffffff;
  font-family: Arial;
  font-size: 22px;
  font-weight: bold;
  padding: 11px 23px;
  width: 300px;
  text-decoration: none;
  text-shadow: 0px -1px 0px #2b665e;
}
</style>
