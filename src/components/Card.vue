<script>
import { nextTick } from 'vue'

export default {
  data() {
    return {
    }
  },
  props: [
    "image_path",
    "title",
    "subtitle",
    "text"
  ],
  emits: ['textBoxSize'],
  methods: {
    emitTextboxSize() {
      this.$emit('textBoxSize', this.$refs.text.offsetTop)
    }
  },
  mounted() {
    this.emitTextboxSize()
  },
  watch: {
    title: {
      handler() {
        this.emitTextboxSize()
      },
      flush: 'post'
    },
    subtitletitle: {
      handler() {
        this.emitTextboxSize()
      },
      flush: 'post'
    },
  }
}
</script>
<template>
  <div class="card-sections">
    <div class="image-container">
      <img v-if="image_path" :src="image_path" @load="emitTextboxSize">
    </div>
    <div class="title-container">
      <h3>{{title}}</h3>
    </div>
    <div class="subtitle-container">
      {{subtitle}}
    </div>
    <div class="text-container" ref="text">
      {{text}}
    </div>>
  </div>
</template>
<style>
.image-container {
  max-height: 200px;
  display: flex;
  justify-content: center;
}
.image-container img {
  max-height: inherit;
  object-fit: scale-down;
}
.title-container {
  padding-top: 2px;
  font: 1.2em "Bookinsanity";
}
.subtitle-container {
  padding-bottom: 4px;
  font: italic 10px/1.2 "Bookinsanity";
}
.text-container {
  overflow-y: clip;
  max-height: 100%;
  font: 10px/1.2 "Bookinsanity"
}
.card-sections {
  max-height: 100%;
  overflow-y: clip;
}
</style>