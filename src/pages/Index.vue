<template>
  <q-page style="margin: 3px auto; width: 700px" class="flex flex-center content-center">
    <div
      v-for="item in imagesList"
      :key="item.id"
      class="q-pa-xs"
    >
      <flip-card
        :image="item"
        @click="flipOnClickHandler($event)"
      />
    </div>
  </q-page>
</template>

<script>
import FlipCard from 'components/FlipCard'
import { defineComponent, ref, onMounted, computed } from 'vue'

export default defineComponent({
  name: 'PageIndex',
  setup () {
    const selectedCard = ref({})
    const imageMap = ref({})
    const imagesList = ref([
      { id: 1, img: 'angularjs.png', flipped: false, pair: 1 },
      { id: 2, img: 'css3.png', flipped: false, pair: 2 },
      { id: 3, img: 'github.png', flipped: false, pair: 3 },
      { id: 5, img: 'html5.png', flipped: false, pair: 4 },
      { id: 6, img: 'mongodb.png', flipped: false, pair: 5 },
      { id: 7, img: 'nodejs.png', flipped: false, pair: 6 },
      { id: 8, img: 'raspberry-pi.png', flipped: false, pair: 7 },
      { id: 9, img: 'stack-overflow.png', flipped: false, pair: 8 },
      { id: 10, img: 'angularjs.png', flipped: false, pair: 1 },
      { id: 11, img: 'css3.png', flipped: false, pair: 2 },
      { id: 12, img: 'github.png', flipped: false, pair: 3 },
      { id: 13, img: 'html5.png', flipped: false, pair: 4 },
      { id: 14, img: 'mongodb.png', flipped: false, pair: 5 },
      { id: 15, img: 'nodejs.png', flipped: false, pair: 6 },
      { id: 16, img: 'raspberry-pi.png', flipped: false, pair: 7 },
      { id: 17, img: 'stack-overflow.png', flipped: false, pair: 8 }
    ])

    const flipOnClickHandler = ({ id, pair }) => {
      const index = imageMap.value[id]

      thereIsCard(index, pair)
    }

    const thereIsCard = (index, pair) => {
      if (!isMatchesCard(pair)) {
        if (indexCard.value.length) {
          setTimeoutHandler()
        }
      } else {
        alert('Good!')
      }
      saveCard(index, pair)
    }

    const indexCard = computed(() => {
      return Object.keys(selectedCard.value)
    })

    const setTimeoutHandler = (timer = 1000) => {
      setTimeout(() => {
        indexCard.value.forEach(index => {
          imagesList.value[index].flipped = false
          selectedCard.value = {}
        })
      }, timer)
    }

    const saveCard = (index, pair) => {
      if (indexCard.value.length < 2) {
        imagesList.value[index].flipped = true
      }
      selectedCard.value[index] = pair
    }

    const isMatchesCard = (pair) => {
      return Object.values(selectedCard.value).includes(pair)
    }

    onMounted(() => {
      imagesList.value.sort(() => Math.random() - 0.5)

      imageMap.value = imagesList.value.reduce((map, obj, index) => {
        map[obj.id] = index
        return map
      }, {})
    })

    return {
      flipOnClickHandler,
      imagesList
    }
  },
  components: {
    FlipCard
  }
})
</script>
