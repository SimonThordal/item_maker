<script>
import Card from './components/Card.vue'
export default {
  components: {Card},
  data() {
    return {
      offsetTop: {
        top: -1
      },
      cards: [{
        image_path: '/src/assets/images/test_image_rect.jpg',
        title: 'Gloves of Being Mean',
        subtitle: 'Uncommon, Requires attunement',
        text: "This kite shield was once part of a shield wall that fell while allowing the evacuation of innocent townsfolk. The agony and blood of that battle seeped into the metal, allowing it to be reforged years later into a reimagined bulwark. When you successfully shove a creature, using the shield to push it, that creature also takes 1d6 necrotic damage. In addition, while holding the shield, you can use an action to shout its command phrase, 'My conviction is greater than your might'. When you do, each hostile creature within 30 feet of you that can hear you must make a DC 15 Wisdom saving throw. Creatures that can't be charmed automatically succeed on the saving throw. On a failed save, a creature is compelled to use its action to attack you on its next turn. If the creature can make multiple attacks on its turn, it makes all of them against you. A creature that fails the saving throw also takes a –2 penalty to its AC until the end of your next turn; for each creature that takes this penalty, you gain a +1 bonus to your AC for the same duration (up to a maximum bonus of +5). Once this property of the shield has been used, it can't be used again until the next dusk or until you take 15 or more necrotic damage from a single hostile attack or magic effect. The wall stood strong as the village fled into the mountains. Holding their ground, the band of soldiers knew this was their final stand. One by one, their brethren fell, and the wall grew more and more narrow. Years later, that same conviction lived within that same metal, now reforged. The memory of that battle was now a timeless stain, but it could never tarnish the desire to protect others."
      },{
        image_path: '/src/assets/images/test_image_square.png',
        title: 'Sentry Candle',
        subtitle: 'Wondrous item, common',
        text: "By using an action to read the mysterious lyrics on this scroll aloud, your words transform into a magical, enchanting song. You can continue to sing from the scroll as an action on each of your following turns for up to 5 minutes. If you sing for at least 1 minute, you gain a +5 bonus to any Charisma (Performance) check you make to sing using the scroll, or a +10 bonus if you sing for the scroll's full duration. When you sing for at least 1 minute using the scroll in this way, you can lace the song with some of your intention. Choose up to three creatures that you can see within 60 feet of you that can hear your performance. Those creatures must make a DC 13 Wisdom saving throw or be charmed by you for 1 hour. This effect ends early on a target if it takes any damage, if you attack it, or if it witnesses you attacking or damaging any of its allies. If a target succeeds on its saving throw, the target has no hint that you tried to charm it.When you stop singing, the words on the scroll fade, and its magic is lost. 'I didn't know you could sing, that was lovely!' 'Aww, thanks! I'm just hoping no one wants an encore.'"
      },]
    }
  },
  methods: {
    positionCardback(size) {
      this.offsetTop.top = -size + "px"
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

.cards-layout {
    margin: 20px
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
