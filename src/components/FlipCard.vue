<template>
  <div :class="flipInTheClasses">
    <div class="flipper" @click.stop="handlerEmit()">
      <q-card class="my-card front">
        <q-card-section>
          <q-img :src="getImage" />
        </q-card-section>
      </q-card>

      <q-card class="my-card back">
        <q-card-section>
          Hey loser
        </q-card-section>
      </q-card>
    </div>
  </div>
</template>

<script>
import { computed } from 'vue'

export default {
  name: 'FlipCard',
  props: {
    image: {
      type: Object,
      require: true
    }
  },
  setup (props, context) {
    const flipInTheClasses = computed(() => props.image.flipped ? 'flip-container' : 'flip-container flipped')

    const getImage = computed(() => {
      return require(`../assets/${props.image.img}`)
    })

    const handlerEmit = () => {
      const { emit } = context
      emit('click', props.image)
    }
    return {
      handlerEmit,
      getImage,
      flipInTheClasses
    }
  }
}
</script>

<style type='text/css' scoped>

/* flip the pane when hovered */
.flipped .flipper {
  transform: rotateY(180deg);
}

.flip-container, .front, .back {
  width: 150px;
  height: 150px;
}
.flip-container {}

/* flip speed goes here */
.flipper {
  transition: 0.6s;
  transform-style: preserve-3d;
  position: relative;
}

/* hide back of pane during swap */
.front, .back {
  backface-visibility: hidden;
  position: absolute;
  top: 0;
  left: 0;
}

/* front pane, placed above back */
.front {
  z-index: 2;
  transform: rotateY(0deg);
}

/* back, initially hidden pane */
.back {
  transform: rotateY(180deg);
}

</style>
