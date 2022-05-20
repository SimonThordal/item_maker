<script>
export default {
    data() {
        return {
            image_path: '/src/assets/images/test_image_rect.jpg'
        }
    }
}
</script>
<template>
    <div class="card-container">
        <div class="card-body">
            <div class="image-container">
                <img v-if="image_path" :src="image_path">
            </div>
            <div class="title-container">
                <h3>Gloves of Being Mean</h3>
            </div>
            <div class="subtitle-container">
                Uncommon, Requires attunement
            </div>
            <div class="text-container">
                London. Michaelmas term lately over, and the Lord Chancellor sitting in Lincoln's Inn Hall. Implacable November weather. As much mud in the streets as if the waters had but newly retired from the face of the earth, and it would not be wonderful to meet a Megalosaurus, forty feet long or so, waddling like an elephantine lizard up Holborn Hill.
            </div>
        </div>
    </div>
</template>
<style>
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
.image-container {
    max-height: 200px;
}
.image-container img {
    max-height: inherit;
    object-fit: scale-down;
}
.title-container {
    padding: 2px 0;
    font: 1.2em "Bookinsanity";
}
.subtitle-container {
    padding: 2px 0;
    font: italic 1em "Bookinsanity";
}
.text-container {
    overflow-y: clip;
    max-height: 100%;
    font: 1em "Bookinsanity"
}
</style>