<template>
  <h1>MEMORY GAMME</h1>
  <section class="gameBoard">
    <Card
      v-for="(card, index) in cardList"
      :key="index"
      :value="card.value"
      :visible="card.visible"
      :matched="card.matched"
      :position="card.position"
      @select-card="flipCard"
    />
  </section>
  <h2>{{ MatchStatus }}</h2>
  <button @click="restartGame" class="ressButton">Reset Gry</button>
</template>

<script>
import _ from "lodash";
import Card from "./components/Card";
import { computed, ref, watch } from "vue";

export default {
  name: "App",
  components: {
    Card,
  },
  setup() {
    const cardList = ref([]);
    const userSelection = ref([]);

    const MatchStatus = computed(() => {
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

    const shuffleCards = () => {
      cardList.value = _.shuffle(cardList.value);
    };

    const restartGame = () => {
      shuffleCards();

      cardList.value = cardList.value.map((card, index) => {
        return {
          ...card,
          position: index,
          matched: false,
          visible: false,
        };
      });
    };

    const cardItems = [
      "#66FFFF",
      "#990033",
      "#FFFF00",
      "#0E0E0E",
      "#76FF03",
      "#1029A1",
      "#696969",
      "#CF7E3C",
    ];
    cardItems.forEach((item) => {
      cardList.value.push({
        value: item,
        visible: false,
        matched: false,
      });

      cardList.value.push({
        value: item,
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

   
  const flipCard = (payload) => {
      cardList.value[payload.position].visible = true;
      if (userSelection.value[0]) {
        if (userSelection.value[0].position === payload.position) {
          return;
        } else {
          userSelection.value[1] = payload;
        }
      } else {
        userSelection.value[0] = payload;
      }
    };

    watch(
      userSelection,
      (currentValue) => {
        if (currentValue.length === 2) {
          const cardFirst = currentValue[0];
          const cardSecond = currentValue[1];
          if (cardFirst.faceValue === cardSecond.faceValue) {
            setTimeout(() => {
              cardList.value[cardFirst.position].matched = true;
              cardList.value[cardSecond.position].matched = true;
            }, 500);
          } else {
            setTimeout(() => {
              cardList.value[cardFirst.position].visible = false;
              cardList.value[cardSecond.position].visible = false;
            }, 500);
          }

          userSelection.value.length = 0;
        }
      },
      { deep: true }
    );
  
    restartGame();

    return {
      cardList,
      flipCard,
      userSelection,
      MatchStatus,
      shuffleCards,
      restartGame,
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
