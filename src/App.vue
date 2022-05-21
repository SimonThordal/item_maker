<script>
import Card from './components/Card.vue'
export default {
  components: {Card},
  data() {
    return {
      cards: [{
        image_path: '/src/assets/images/test_image_rect.jpg',
        title: 'Gloves of Being Mean',
        subtitle: 'Uncommon, Requires attunement',
        text: "London. Michaelmas term lately over, and the Lord Chancellor sitting in Lincoln's Inn Hall. Implacable November weather. As much mud in the streets as if the waters had but newly retired from the face of the earth, and it would not be wonderful to meet a Megalosaurus, forty feet long or so, waddling like an elephantine lizard up Holborn Hill."
      },{
        image_path: '/src/assets/images/test_image_square.png',
        title: 'Sentry Candle',
        subtitle: 'Uncommon',
        text: "This dark candle has a crenelated rim that remains even as the candle melts. While lit, small windows seemingly glow from within the candle's dark wax. The candle's magic is activated when the candle is lit, which requires an action. After burning for 8 hours, the candle is destroyed. You can snuff it out early for use at a later time. Moving the lit candle immediately snuffs it. Deduct the time it burned in increments of 1 minute from the candle's total burn time. While lit, the candle sheds dim light in a 15-foot radius. Any creature within that light is mentally alerted whenever another Tiny or larger creature enters the area within 60 feet of the candle."
      }]
    }
  }
}
</script>

<template>
  <main>
    <div class="cards-layout">
      <div class="card-container" v-for="card in cards">
          <div class="card-body">
            <Card v-bind="card"/>
          </div>
      </div>
    </div>
  </main>
</template>

<style>
@import './assets/base.css';

.card-container {
    padding: 5px
}
.card-body {
    height: 475px;
    width: 275px;
    border: 2px solid;
    padding: 5px;
    overflow-y:clip;
}

@media print {
  .cards-layout {
    display: flex;
  }
}
</style>
