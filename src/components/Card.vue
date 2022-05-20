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
            <div class="text-container"></div>
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
}
.image-container {
    max-height: 200px;
}
.image-container img {
    max-height: inherit;
    object-fit: scale-down;
}
</style>