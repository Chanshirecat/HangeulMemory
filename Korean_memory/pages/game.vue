<template>
    <div>
      <h1>Hangeul Memory</h1>
      <section class="game-board">
        <Card
        v-for="(card, index) in cardList" 
        :key="`card${index}`"
        :value="card.value"
        :visible="card.visible"
        :position="card.position"
        @select-card="flipCard"
        />
      </section>

      <button>Start Game</button>
    </div>
  </template>

  <script>
  import { ref } from 'vue'
import Card from '~~/components/Card.vue';

export default {
  name: 'App',
  components: {
    Card
  },
  setup() {
    const cardList = ref([])

    for (let i = 0; i < 40; i++) {
      cardList.value.push({
        value: i,
        visible: false,
        position: 
      })
    }

    const flipCard = (payload) => {
      cardList.value[payload.position].visible = true;
    }

    return {
      cardList,
      flipCard,
    }
  }
}

</script>

<style>
#app {
}

.card {
  border: 40px solid #0F64CD;
  border-radius: 100px;
}

.game-board {
  display: grid;
  grid-template-columns: 50px 50px 50px 50px 50px 50px 50px 50px;
  grid-template-rows: 50px 50px 50px 50px 50px;
  grid-column-gap: 55px;
  grid-row-gap: 55px;
  justify-content: center;
}
</style>
  