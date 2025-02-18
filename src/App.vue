<script setup>
import jsonData from "./data.json";
import recipe from "./components/recipe.vue";
import cart from "./components/cart.vue";

const datas = jsonData;
</script>

<template>
    <main>
        <h1>Desserts</h1>
        <recipe
            v-for="data in datas"
            :image="data.image.mobile"
            :category="data.category"
            :name="data.name"
            :price="data.price"
        />
        <cart />
    </main>
</template>

<style scoped></style>
