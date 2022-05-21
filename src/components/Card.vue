<script>
export default {
    data() {
        
    },
    props: [
        "image_path",
        "title",
        "subtitle",
        "text"
    ]
}
</script>
<template>
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
</template>
<style>
.image-container {
    max-height: 200px;
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
    font: italic 1em "Bookinsanity";
}
.text-container {
    overflow-y: clip;
    max-height: 100%;
    font: 1em "Bookinsanity"
}
</style>