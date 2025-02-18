<script setup>
defineProps(["image", "category", "name", "price"]);
</script>

<template>
    <div>Recipe</div>
    <p>{{ image }}</p>
    <p>{{ category }}</p>
    <p>{{ name }}</p>
    <p>{{ price }}</p>
</template>

<style scoped></style>
