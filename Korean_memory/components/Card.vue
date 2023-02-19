<script>
export default {
    props: {
        position: {
            type: Number,
            required: true,
        },
        value: {
            type: Number,
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
        <div v-if="visible" class="card-face.is-front">
            {{ value }}
        </div>
        <div v-else class="card-face.is-back">
            Back
        </div>
    </div>
</template>

<style>
.card {
  border-radius: 100px;
  position: relative;
}

.card-face {
    width: 100%;
    height: 100%;
    position: absolute;
}

.card-face, .is-front {
    background-color: #CD2E3A;
    color: white;
}

.card-face, .is-back {
    background-color: #0F64CD;
    color: white;
}
</style>