<script>
import { nextTick } from 'vue'
export default {
  data() {
    return {
      _image_path: this.image_path,
      lineHeight: 12,
      canvas: null,
      spaceWidth: 0,
    }
  },
  props: [
    "image_path",
    "title",
    "subtitle",
    "text"
  ],
  emits: ['reportContent', 'propertyUpdate'],
  mounted() {
    this.spaceWidth = this.getTextWidth(" ", this.getCanvasFont(this.$refs.text_body))
  },
  methods: {
    getTextWidth(text, font) {
      // re-use canvas object for better performance
      this.canvas = this.canvas || (this.canvas = document.createElement("canvas"));
      const context = this.canvas.getContext("2d");
      context.font = font;
      const metrics = context.measureText(text);
      return metrics.width;
    },
    getCssStyle(element, prop) {
        return window.getComputedStyle(element, null).getPropertyValue(prop);
    },
    getCanvasFont(el = document.body) {
      const fontWeight = this.getCssStyle(el, 'font-weight') || 'normal';
      const fontSize = this.getCssStyle(el, 'font-size') || '16px';
      const fontFamily = this.getCssStyle(el, 'font-family') || 'Times New Roman';
      return `${fontWeight} ${fontSize} ${fontFamily}`;
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
      this.report()
    },
    endEdit(e, property) {
      if (e.shiftKey) {
        this.edit(e, property)
        return
      }
      e.target.blur(e, property)
    },
    updateProperty(property, value) {
      this.$emit('propertyUpdate', [property, value])
    },
    lineText(text, lineLength) {
      // Given a string and the lineLength, returns the words on the next line
      // and the remaining string
      const tokens = text.split(/((?<=\s)\b)|$/mug)
      let line = ""
      let l = 0
      while (tokens.length > 0) {
        const token = tokens[0]
        if (token == undefined) {
          return [line, tokens.join("")]
        }
        const tokenWidth = this.getTextWidth(token, this.getCanvasFont(this.$refs.text_body))
        if ((tokenWidth + l) > lineLength + this.spaceWidth) {
          break
        }
        tokens.shift()
        line += token
        l += tokenWidth
      } 
      return [line, tokens.join("")]
    },
    lines() {
      let remainder = this.$refs.text_body.innerText
      let line = ""
      let lines = []
      do {
        [line, remainder] = this.lineText(remainder, this.lineLength())
        lines.push(line)
      } while(remainder.length > 0)
      return lines
    },
    lineLength() {
      return Math.ceil(this.$refs.text_body.offsetWidth)
    },
    maxLines() {
      let elHeight = this.$refs.text_container.clientHeight
      return Math.floor(elHeight / this.lineHeight)
    },
    nLines() {
      let elHeight = this.$refs.text_body.offsetHeight
      return Math.floor(elHeight / this.lineHeight)
    },
    textLength() {
      let text = this.$refs.text_body.innerText
      return this.getTextWidth(text, this.getCanvasFont(this.$refs.text_body))
    },
    report() {
      this.$emit('reportContent', [this.maxLines(), this.lines()])
    }

  }
}
</script>
<template>
  <div class="card-container" ref="card_container">
    <div class="image-container"
      @drop.prevent="dropImage"
      @dragenter.prevent @dragover.prevent
    >
      <img ref="image_container" v-if="_image_path" :src="_image_path" @drop="dropImage">
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
    <div ref="text_container" class="text-container">
      <div contenteditable ref="text_body" class="text-body editable"
        @keyup.stop.prevent="edit($event, 'text')"
        @keydown.enter="endEdit($event, 'text')">
        {{text}}
      </div>
    </div>
  </div>
</template>
<style>
.card-container {
  height: 100%;
  overflow-y: clip;
  display: flex;
  flex-direction: column;
}
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
  flex-grow: 1;
  overflow-y: clip;
}
.text-body {
  overflow-y: clip;
  font: 10px/1.2 "Bookinsanity"
}
</style>