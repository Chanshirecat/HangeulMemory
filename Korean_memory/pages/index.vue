<template>
    <div class="app">
    <h1>Hangeul Memory</h1>
  
    <TransitionGroup tag="section" class="game-board" name="shuffle-card">
      <Card v-for="card in cardList" 
      :key="`card-${card.value}-${card.variant}`"
      :value="card.value"
      :matched="card.matched"
      :visible="card.visible"
      :position="card.position"
      @select-card="flipCard"/>
    </TransitionGroup>
  
    <h2>{{ status }}</h2>
  <div id="buttons">
    <button id="restartBtn" @click="restartGame">Restart Game</button>
</div>
</div>
  </template>
  
  
  <script>
  
  import _ from 'lodash'
  import { computed, ref, watch } from 'vue'
  import { Card } from '#components'

  export default {
    name:'App',
    components: {
      Card
    },
    setup() {
      const cardList = ref([])
      const userSelection = ref([])
      const status = computed(() => {
        if (remainingPairs.value === 0) {
          return 'You win!'
        } else {
          return `Remaining Pairs: ${remainingPairs.value}`
        }
      })
      const remainingPairs = computed(() => {
         const remainingCards = cardList.value.filter
         (card => card.matched === false).length
         return remainingCards / 2 
      })
    
      function shuffleCards() {
        cardList.value.sort(() => {
        return 0.5 - Math.random();
       });
       return cardList.value;
      }
      const restartGame = () => {
        shuffleCards()
        cardList.value = cardList.value.map((card, index) => {
          return {
            ...card, 
            matched: false,
            position: index,
            visible: false,
          }
        })
      }
      
      const cardItems = ['1', '2', '3', '4', '5', '6', '7', '8','9', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19','20', '21', '22', '23', '24', '25', '26', '27']
      cardItems.forEach(item => {
        cardList.value.push({
          value: item,
          variant: 1,
          visible: false,
          position: null,
          matched: false
        })
        cardList.value.push({
          value: item,
          variant: 2,
          visible: false,
          position: null,
          matched: false
        })
      })
      
      shuffleCards() 
      cardList.value.forEach((card, index) => {
       card.position = index;
      });
    
      const flipCard = payload => {
        cardList.value[payload.position].visible = true
        if (userSelection.value[0]) {
         if (userSelection.value[0].position === payload.position && userSelection.value[0].faceValue === payload.faceValue) {
          return 
         } else {
          userSelection.value[1] = payload
         }
        } else {
          userSelection.value[0] = payload
        }
      }

      watch(userSelection, (currentValue) => {
         if (currentValue.length === 2) {
          const cardOne = currentValue[0]
          const cardTwo = currentValue[1] 
          if (cardOne.faceValue === cardTwo.faceValue){
            
             cardList.value[cardOne.position].matched = true
             cardList.value[cardTwo.position].matched = true 
          } else {
            setTimeout(() => {
              cardList.value[cardOne.position].visible = false
              cardList.value[cardTwo.position].visible = false 
            }, 1000)
          }
          userSelection.value.length = 0 
         }
      }, 
      {deep: true})
      return {
        cardList,
        flipCard, 
        userSelection, 
        status, 
        shuffleCards, 
        restartGame, 
      }
    }
  }
  </script>
  
  
  <style>

@import url('https://fonts.googleapis.com/css2?family=Mynerve&display=swap');

  html{
    background-image: url('../public/images/background.jpg');
    background-size: cover;
  }

  #app {
    font-family: 'Mynerve', cursive;
    text-align: center;
    color:#0F64CD; 
  } 

  h1, h2 {
    font-family: 'Mynerve', cursive;
    text-align: center;
  }

  .status {
    font-family: 'Mynerve', cursive;
    font-size: 18px;
  }

  .game-board{
    display: grid; 
    grid-template-columns: repeat(9, 50px); 
    grid-template-rows: repeat(4, 50px);
    gap: 50px;
    justify-content: center;
  }
  .shuffle-card-move{
     transition: transform 0.8s ease-in; 
  }
  #restartBtn{
    color:#CD2E3A;
    border-radius: 5px;
    border-color:black;
    font-size: 20px; 
    padding: 8px; 
    transition-duration: 0.4s;
    font-family: 'Mynerve', cursive;
  }
  #restartBtn:hover{
    color: white; 
    background-color: #ff3c4c;
    cursor:pointer; 
  }

  #buttons {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
  }
  </style>