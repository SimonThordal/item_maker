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
        <h3>{{title}}</h3>
    </div>
    <div class="subtitle-container">
        {{subtitle}}
    </div>
    <div class="text-container">
        {{text}}
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
    font: italic 1em "Bookinsanity";
}
.text-container {
    overflow-y: clip;
    max-height: 100%;
    font: 1em "Bookinsanity"
}
</style>