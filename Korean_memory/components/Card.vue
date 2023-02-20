<script>
import { computed } from 'vue'

export default {
    props: {
        matched: {
            type: Boolean,
            default: false,
        },
        position: {
            type: Number,
            required: true,
        },
        value: {
            type: String,
            required: true,
        },
        visible: {
            type: Boolean,
            default: false,
        }
    },
    setup(props, context) {
        const flippedStyles = computed(() => {
            if (props.visible) {
                return 'is-flipped';
            }
        })
        const selectCard = () => {
            context.emit('select-card', {
                 position: props.position,
                 faceValue: props.value,
            })
        }

        return {
            flippedStyles,
            selectCard
        }
}
}
</script>

<template>
    <div class="card" _class="flippedStyles" @click="selectCard">
        <div class="card-face is-front">
            <img :src="`/images/${value}.png`" :alt="value" class="Hangeul">
            <img v-if="match" src="/images/sejong-ocon.png" class="checkmark">
        </div>
        <div class="card-face is-back">
        </div>
    </div>
</template>

<style>


.card {
  border-radius: 10px;
  position: relative;
  align-items: center;
transition: 0.5s transform ease-in;
transform-style: preserve-3d;
}

.card.is-flipped {
    transform: rotateY(180deg);
}

.card-face {
    width: 100%;
    height: 100%;
    position: absolute;
    background-size: 50px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-color: #CD2E3A;
    border-radius: 10px;
    backface-visibility: hidden;
}

.card-face.is-front {
    background-size: 50px;
    align-content: center;
    size: 50px;
    border-radius: 10px;
    border-color: #CD2E3A;

}

.card-face.is-back {
    background-image: url("/images/sejong-ocon.png");
    background-color: #0F64CD;
    background-size:contain;
    border-radius: 10px;
    transform: rotateY(180deg);
}

.checkmark {
    position: absolute;
    right: 10px;
    border: 5px;
}
</style>