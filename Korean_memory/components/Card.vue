<script>
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
        const selectCard = () => {
            context.emit('select-card', {
                 position: props.position,
                 faceValue: props.value,
            })
        }

        return {
            selectCard
        }
}
}
</script>

<template>
    <div class="card" @click="selectCard">
        <div v-if="visible" class="card-face is-front">
            <img :src="`/images/${value}.png`" :alt="value" class="Hangeul">
            <img v-if="match" src="/images/sejong-ocon.png" class="checkmark">
        </div>
        <div v-else class="card-face is-back">
        </div>
    </div>
</template>

<style>


.card {
  border-radius: 5px;
  position: relative;
  align-items: center;
  border: 2px solid black;
    border-radius: 10px;
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
}

.card-face.is-front {
    background-size: 50px;
    align-content: center;
    size: 50px;
    border-radius: 2px;
    border-color: #CD2E3A;

}

.card-face.is-back {
    background-image: url("/images/sejong-ocon.png");
    background-color: #0F64CD;
    background-size:cover;
    border-radius: 10px;
}

.checkmark {
    position: absolute;
    right: 10px;
    border: 5px;
}
</style>