<template>
  <div class="container">
    <div class="relative flex flex-col my-10">
      <div class="head-text absolute">
        <h4 class="text-xs md:text-sm text-gray-600 font-semibold">
          THE PEOPLE BEHIND THE BUNNY
        </h4>
        <h1
          class="text-xl md:text-2xl lg:text-4xl leading-5 md:leading-6 lg:leading-10 font-extrabold text-black"
        >
          Hopper is a culture of<br />
          makers. We build things.
        </h1>
      </div>
      <div class="flex items-end">
        <div ref="block-1" class="block-box block-1"></div>
        <div ref="block-2" class="block-box block-2"></div>
        <div ref="block-3" class="block-box block-3"></div>
      </div>
      <div class="flex items-start">
        <div ref="block-4" class="block-box block-4"></div>
        <div ref="block-5" class="block-box block-5"></div>
        <div ref="block-6" class="block-box block-6"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    images: {
      type: Array,
      default: () => [],
    },
  },
  beforeMount() {
    this.images = this.shuffle(this.images)
  },
  mounted() {
    this.placeRandomImage()
  },
  methods: {
    shuffle(array) {
      let currentIndex = array.length
      let temporaryValue = null
      let randomIndex = null

      while (currentIndex !== 0) {
        randomIndex = Math.floor(Math.random() * currentIndex)
        currentIndex -= 1

        temporaryValue = array[currentIndex]
        array[currentIndex] = array[randomIndex]
        array[randomIndex] = temporaryValue
      }

      return array
    },
    placeRandomImage() {
      let count = 0
      Object.keys(this.$refs).forEach((key) => {
        this.$refs[key].style.background = `url(${this.imageURL(count)})`
        this.$refs[key].style.backgroundSize = 'cover'
        count++
      })
    },
    imageURL(index) {
      return require(`~/assets/images/${this.images[index]}`)
    },
  },
}
</script>

<style lang="scss" scoped>
.head-text {
  top: 13%;
}

.block-box {
  @apply shadow;

  background-size: cover;
  margin: 0.3rem;
  border-radius: 8px;
}

.block-1 {
  width: 31%;
  padding-top: 22%;
  margin-bottom: -100px;
}

.block-2 {
  width: 19.75%;
  padding-top: 19.75%;
}

.block-3 {
  width: 48.68%;
  padding-top: 48.68%;
}

.block-4 {
  width: 20%;
  padding-top: 16%;
  margin-top: 110px;
  margin-left: 10.8%;
}

.block-5 {
  width: 30%;
  padding-top: 30%;
}

.block-6 {
  width: 30%;
  padding-top: 20%;
}
</style>
