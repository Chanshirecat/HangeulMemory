<template>
    <div id="app">



        <h1>Hangeul Memory</h1>



        <section class="game-board">



            <Card v-for="(card, index) in cardList" :key="`card${index}`" :match="card.match" :value="card.value"
                :visible="card.visible" :position="card.position" @select-card="flipCard" />



        </section>



        <h2>{{ status }}</h2>

        <button @click="restartGame" class="button">Restart the Game</button>
        <p>Nathalie Klinger | cc211040</p>
    </div>
</template>

<script>
import { computed, ref, watch, } from 'vue'
import _ from 'lodash'
import Card from '~~/components/Card.vue';

export default {
    name: 'App',
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
            const remainingCards = cardList.value.filter(
                card => card.match === false).length

            return remainingCards / 2;
        })

        const shuffleCards = () => {
            cardList.value = _.shuffle(cardList.value)
        }

        const restartGame = () => {
            shuffleCards()

            cardList.value = cardList.value.map((card, index) => {
                return {
                    ...card,
                    match: false,
                    position: index,
                    visible: false,
                }
            })
        }

        const cardItems = ['1', '2', '3', '4', '5', '6', '7', '8', '9', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19', '20', '21', '22', '23', '24', '25', '26', '27']

        cardItems.forEach(item => {
            cardList.value.push({
                value: item,
                visible: false,
                position: null,
                match: false,
            })

            cardList.value.push({
                value: item,
                visible: false,
                position: null,
                match: false,
            })
        })

        cardList.value = cardList.value.map((card, index) => {
            return {
                ...card,
                position: index,
            }
        })

        const flipCard = payload => {
            cardList.value[payload.position].visible =
                true;

            if (userSelection.value[0]) {
                if (
                    (userSelection.value[0].position ===
                    payload.position) &&
                     (userSelection.value[0].faceValue === 
                     payload.faceValue)
                     ) {
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
                const firstCard = currentValue[0]
                const secondCard = currentValue[1]

                if (firstCard.faceValue === secondCard.faceValue) {

                    cardList.value[firstCard.position]
                        matched = true
                    cardList.value[secondCard.position]
                        matched = true
                } else {
                    setTimeOutcard(() => {
                        List.value[firstCard.position].visible = firstCard.visible = false
                        cardList.value[secondCard.position].visible = secondCard.visible = false
                    }, 1000)
                }

                userSelection.value.length = 0
            }
        }, { deep: true })

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

#app {
    background-image: url(./public/images/background.jpg);
    background-size: cover;
    text-align: center;
    font-family: 'Mynerve', cursive;
    
}


.game-board {
    display: grid;
    grid-template-columns: repeat(9, 50px);
    grid-template-rows: repeat(6, 50px);
    grid-column-gap: 50px;
    grid-row-gap: 50px;
    justify-content: center;
}

.button {
    border-radius: 10px;
    color: white;
    padding: 1rem;
    background-color: #CD2E3A;
    font-family: 'Mynerve', cursive;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto;
}

</style>
  