<template>
    <div>
      <h1>Hangeul Memory</h1>
      <section class="game-board">
        <Card
        v-for="(card, index) in cardList" 
        :key="`card${index}`"
        :value="card"
        />
      </section>
      
      <button>Start Game</button>
    </div>
  </template>

  <script>
import Card from '~~/components/Card.vue';

export default {
  name: 'App',
  components: {
    Card
  },
  setup() {
    const cardList = []

    for (let i = 0; i < 40; i++) {
      cardList.push(i)
    }

    return {
      cardList
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
  