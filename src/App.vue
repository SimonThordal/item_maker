<script>
import Card from './components/Card.vue'
export default {
  components: { Card },
  data() {
    return {
      defaultCard: {
        image_path: 'assets/images/placeholder_sword.png',
        title: 'Sword of Placeholding',
        subtitle: 'Uncommon, Requires attunement',
        text: "Double click any text in the card to change it. Overflowing text will be printed on the back of the card.",
        backText: ""
      },
      cards: []
    }
  },
  mounted() {
    this.addCard()
  },
  methods: {
    addCard() {
      if (this.cards.length >= 4) {
        alert('You cannot add more than 4 cards')
        return;
      }
      this.cards.push({...this.defaultCard})
    },
    updateProperty(cardIndex, property, value) {
      let card = this.cards[cardIndex]
      card[property] = value
    },
    updateCardContent(cardIndex, maxLines, lines) {
      const card = this.cards[cardIndex]
      let backText = ""
      lines.slice(maxLines).forEach(line => {
        backText += line
      });
      card.backText = backText
      if (lines.length == maxLines + 1 && backText.length == 1) {
        console.log("Replace cursor!")
      }
    }
  }
}
</script>

<template>
  <main>
    <div class="cards-layout">
      <div class="card-body" v-for="(card, i) in cards">
        <Card v-bind="card" @report-content="updateCardContent(i,...$event)" @property-update="updateProperty(i, ...$event)"/>
      </div>
      <div class="add-button" @click="addCard">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><!--! Font Awesome Pro 6.1.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M432 256c0 17.69-14.33 32.01-32 32.01H256v144c0 17.69-14.33 31.99-32 31.99s-32-14.3-32-31.99v-144H48c-17.67 0-32-14.32-32-32.01s14.33-31.99 32-31.99H192v-144c0-17.69 14.33-32.01 32-32.01s32 14.32 32 32.01v144h144C417.7 224 432 238.3 432 256z"/></svg>
      </div>
    </div>
    <div class="page-break cards-layout cardbacks-layout">
      <div class="card-body cardback" v-for="(card, i) in cards">
        <div contenteditable>
          {{card.backText}}
        </div>
      </div>
    </div>

  </main>
</template>

<style>
@import '/assets/base.css';

.add-button {
  height: inherit;
  width: 50px;
  display: flex;
}
.cards-layout {
  display: flex;
}
.card-body {
  width: 2.75in;
  height: 4.75in;
  border: 2px solid;
  border-radius: 10px;
  padding: 5px;
  padding-bottom: 14px;
  margin: 5px;
  white-space: pre-wrap;
}

.gridded {
  columns: 2 2.75in;
  column-gap: 2ch;
  column-rule: 0ch;
  column-span: all;
}

.page-break {
  page-break-before: always;
}

.cardback {
  overflow-y: clip;
  max-height: 100%;
  font: 10px/1.2 "Bookinsanity";
  outline: 2px solid;
}

@media print {
  .cards-layout {
    display: flex;
    flex-flow: row wrap;
  }
  .cardbacks-layout {
    flex-flow: row-reverse wrap;
  }
  .add-button {
    display: none;
  }
}
</style>
