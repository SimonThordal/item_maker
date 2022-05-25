<script>
import Card from './components/Card.vue'
export default {
  components: {Card},
  data() {
    return {
      offsetTop: {
        top: -1
      },
      defaultCard: {
        image_path: '/src/assets/images/test_image_rect.jpg',
        title: 'Sword of Placeholding',
        subtitle: 'Uncommon, Requires attunement',
        text: "Double click any text in the card to change it. Overflowing text will be printed on the back of the card."
      },
      cards: []
    }
  },
  mounted() {
    this.addCard()
  },
  methods: {
    positionCardback(size) {
      this.offsetTop.top = -size + "px"
    },
    addCard() {
      this.cards.push(this.defaultCard)
    }
  }
}
</script>

<template>
  <main>
    <div class="cards-layout">
      <div class="card-body" v-for="card in cards">
        <Card v-bind="card" @text-box-size="positionCardback"/>
      </div>
      <div class="add-button" @click="addCard">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><!--! Font Awesome Pro 6.1.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M432 256c0 17.69-14.33 32.01-32 32.01H256v144c0 17.69-14.33 31.99-32 31.99s-32-14.3-32-31.99v-144H48c-17.67 0-32-14.32-32-32.01s14.33-31.99 32-31.99H192v-144c0-17.69 14.33-32.01 32-32.01s32 14.32 32 32.01v144h144C417.7 224 432 238.3 432 256z"/></svg>
      </div>
    </div>
    <div class="page-break cards-layout cardbacks-layout">
      <div class="card-body cardback" v-for="card in cards">
        <div class="top-border"></div>
        <div class="offset-text" :style="offsetTop">
          {{card.text}}
        </div>
      </div>
    </div>
  </main>
</template>

<style>
@import './assets/base.css';

.add-button {
  height: 100%;
  width: 50px;
}
.cards-layout {
    margin: 20px;
    display: flex;
}
.card-body {
    height: 475px;
    width: 275px;
    border: 2px solid;
    padding: 5px;
    padding-bottom: 12px; 
}
.page-break {
  page-break-before: always;
}
.cardbacks-layout {
  margin: 20px;
}
.cardback {
  outline: 2px solid;
  overflow-y: clip;
  max-height: 100%;
  font: 10px/1.2 "Bookinsanity";
  padding-top: 0px;
}
.top-border {
  z-index: 999;
  height: 12px;
  background-color: white;
}
.offset-text {
  padding-top: 35px;
  padding-right: 5px;
  position:absolute;
  top:-0;
}
@media print {
  .cards-layout {
    display: flex;
    flex-flow: row wrap;
  }
  .cardbacks-layout {
    flex-flow: row-reverse wrap;
  }
}
</style>
