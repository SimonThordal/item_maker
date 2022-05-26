<script>

export default {
  data() {
    return {
      _image_path: this.image_path,
    }
  },
  props: [
    "image_path",
    "title",
    "subtitle",
    "text"
  ],
  emits: ['textBoxSize', 'propertyUpdate'],
  methods: {
    emitTextboxSize() {
      this.$emit('textBoxSize', this.$refs.text.offsetTop)
    },
    dropImage(e) {
      const dt = e.dataTransfer;
      const files = dt.files;
      let file  = files[0];
      if (!file.type.startsWith('image/')){ 
        alert('It seems you dropped a non-image file. Please try with another image.')
      }
      let img = this.$refs.image_container;
      img.file = file;
      const reader = new FileReader();
      reader.onload = (function(aImg) { return function(e) { aImg.src = e.target.result; }; })(img);
      reader.readAsDataURL(file);
    },
    edit(e, property) {
      let src = e.target.innerText;
      this.updateProperty(property, src)
    },
    endEdit(e, property) {
      if (e.shiftKey) {
        return
      }
      e.target.blur(e, property)
    },
    updateProperty(property, value) {
      this.$emit('propertyUpdate', [property, value])
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
    <div class="image-container"
      @drop.prevent="dropImage"
      @dragenter.prevent @dragover.prevent
    >
      <img ref="image_container" v-if="_image_path" :src="_image_path" @load="emitTextboxSize" @drop="dropImage">
    </div>
    <div class="title-container editable">
      <h3 contenteditable
        @blur="edit($event, 'title')"
        @keydown.enter="endEdit($event, 'title')"
        >{{title}}</h3>
    </div>
    <div class="subtitle-container editable" contenteditable
      @blur="edit($event, 'subtitle')"
      @keydown.enter="endEdit($event, 'subtitle')">
      {{subtitle}}
    </div>
    <div contenteditable class="text-container editable"
      @blur="edit($event, 'text')"
      @keydown.enter="endEdit($event, 'text')"
      ref="text">
      {{text}}
    </div>
  </div>
</template>
<style>
.editable {
  white-space: pre-wrap
}
.image-container {
  max-width: 100%;
  display: flex;
  justify-content: center;
}
.image-container img {
  max-width: 100%;
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