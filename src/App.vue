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
      }]
    }
  }
}
</script>

<template>
  <main>
    <div class="card-container" v-for="card in cards">
        <div class="card-body">
          <Card v-bind="card"/>
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
}
</style>
