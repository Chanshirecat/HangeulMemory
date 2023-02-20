<script>
import {computed} from "vue"; 

export default {
  props: {
    matched: {
        type: Boolean,
        default: false
    },
    position: {
        type: Number,
        required: true
    },
    value: {
        type: String, 
        required: true
    },
    visible: {
    type: Boolean,
    default: false
    }
  },
  setup(props, context) {
    const flippedStyles = computed(() => {
        if (props.visible) {
            return 'is-flipped'
        }
    })
    const selectCard = () => {
     context.emit('select-card', {
        position: props.position,
        faceValue: props.value
     })
    }
    return {
        flippedStyles,
        selectCard,
    }
  }
}
</script>

<template>
   <div class="card" :class="flippedStyles" @click="selectCard">

    <div class="card-face is-front">
        <img :src="`/images/${value}.png`" class="pictures" :alt="value">
    </div>

    <div class="card-face is-back"></div>

    </div>
</template>

<style>
.card{
  position: relative; 
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
   border-radius: 10px;
   backface-visibility: hidden;
}
.card-face.is-front {
   transform: rotateY(180deg);
}
.card-face.is-back {
    background-image: url('/public/images/sejong-ocon.png');
    background-color: #0F64CD;
    background-size: cover;  
}
.card-image {
    width: inherit;
    height: inherit; 
}
.pictures {
    width: inherit;
    height: inherit; 
    border-color: #0F64CD;
   border-radius: 10px;
} 
</style>