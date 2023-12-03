<template>
  <transition
    enter-from-class="opacity-0"
    enter-active-class="transition duration-300"
    leave-to-class="opacity-0"
    leave-active-class="transition duration-300"
  >
    <div v-if="showResult">
      <div
        @click="onToggleShowResult"
        class="absolute bg-black opacity-70 inset-0 z-10"
      ></div>
      <div class="absolute w-full p-4">
        <div
          class="w-full max-w-lg p-3 relative mx-auto my-auto rounded-xl shadow-lg bg-white z-20"
        >
          <div>
            <div class="text-center p-3 flex-auto justify-center leading-6">
              <img :src="selectedItem?.image" alt="" class="m-auto" />
              <div v-if="selectedItem?.value">
                <h2 class="text-2xl font-bold py-4">Congratulations</h2>
                <p class="text-md px-8 mb-4">
                  <strong>You have won.....</strong>Try out our spin and win
                  game to win one of our exciting prizes.
                </p>
              </div>
              <div v-else>
                <h2 class="text-2xl font-bold py-4">Oh no</h2>
                <p class="text-md px-8 mb-4">
                  <strong>Try again.....</strong> Try out our spin and win game
                  to win one of our exciting prizes.
                </p>
              </div>

              <button
                @click="onToggleShowResult"
                class="bg-yellow-500 hover:bg-yellow-700 font-bold py-1 px-8 rounded-full"
              >
                TRY AGAIN
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </transition>

  <div ref="container" class="flex items-center justify-center spin-container">
    <div
      class="icon flex items-center justify-center shadow-lg"
      @click="spin"
      @keyup.enter="spin"
      @keyup.space="spin"
      tabindex="0"
    >
      PLAY
    </div>
  </div>
</template>

<script setup lang="ts">
import random from 'random'
import { Wheel } from 'spin-wheel/dist/spin-wheel-esm'
import { onMounted, ref } from 'vue'

const properties = {
  isInteractive: false,
  radius: 0.94,
  itemLabelRadius: 0.8,
  itemLabelRotation: 90,
  itemLabelAlign: 'center',
  itemLabelColors: ['#fff'],
  itemLabelBaselineOffset: -0.4,
  itemLabelFontSizeMax: 22,
  itemBackgroundColors: [
    '#fdc963',
    '#00cca8',
    '#2b87e9',
    '#fd775b',
    '#ff4b78',
    '#c88857',
    '#a64a97',
    '#5b7c7d',
    '#715344',
    '#904e55',
    '#8b7856',
  ],
  overlayImage: 'src/assets/overlay.svg',
  rotationSpeedMax: 2000,
  lineWidth: 1,
  lineColor: 'white',
  items: [
    {
      label: 'BEER',
      image: 'src/assets/beer.svg',
      value: 3,
    },
    {
      label: 'COIN',
      image: 'src/assets/coin.svg',
      value: 1,
    },
    {
      label: 'ICE CREAM',
      image: 'src/assets/ice-cream.svg',
      value: 5,
    },
    {
      label: 'GIFT',
      image: 'src/assets/gift.svg',
      value: 2,
    },
    {
      label: 'COIN',
      image: 'src/assets/coin.svg',
      value: 1,
    },
    {
      label: 'COIN',
      image: 'src/assets/coin.svg',
      value: 1,
    },
    {
      label: 'LOSE',
      image: 'src/assets/sad.svg',
      value: 0,
    },
  ],
}

const container = ref()
const spinCount = ref(0)
const selectedItem = ref<
  { label: string; image: string; value: number } | undefined
>(undefined)
const showResult = ref(false)

let wheel: Wheel | undefined = undefined

const spin = () => {
  if (!wheel) return
  if (spinCount.value > 2) return

  spinCount.value += 1

  wheel.onCurrentIndexChange = () => {
    if (!wheel) return

    switch (true) {
      case wheel.rotationSpeed < 400:
        wheel.rotationResistance = -100
        break
      case wheel.rotationSpeed < 100:
        wheel.rotationResistance = -30
        break
      case wheel.rotationSpeed < 30:
        wheel.rotationResistance = -10
        break
    }
  }

  wheel.rotationResistance = -400
  wheel.spin(wheel.rotationSpeed + random.int(800, 1200))
}

const onToggleShowResult = () => {
  showResult.value = !showResult.value
  selectedItem.value = undefined
}

const openCongratulationDialog = ($event: {
  type: 'rest'
  currentIndex: number
  rotation: number
}) => {
  onToggleShowResult()
  spinCount.value = 0
  selectedItem.value = properties.items[$event.currentIndex]
}

onMounted(() => {
  wheel = new Wheel(container.value, {
    ...properties,
  })

  wheel.spin(10)

  wheel.onRest = ($event) => {
    if (!spinCount.value) return
    openCongratulationDialog($event)
  }

  wheel.onSpin = () => {}
})
</script>

<style lang="css" scoped>
.spin-container {
  aspect-ratio: 1/1;
  height: 100vw;
  max-height: 780px;
  position: relative;
}

.button-container {
  margin-top: -5.5rem;
}

.icon {
  cursor: pointer;
  width: 80px;
  height: 80px;
  border-radius: 50%;
  background-color: white;
  position: relative;
  font-weight: 600;
  z-index: 1;
}
</style>
