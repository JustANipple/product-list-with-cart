<script setup>
import jsonData from "./data.json";
import recipe from "./components/recipe.vue";
import cart from "./components/cart.vue";

const datas = jsonData;
</script>

<template>
    <main>
        <h1>Desserts</h1>
        <div>
            <recipe
                v-for="data in datas"
                :image="data.image.mobile"
                :category="data.category"
                :name="data.name"
                :price="data.price"
            />
        </div>
        <cart />
    </main>
</template>

<style scoped>
main {
    background-color: var(--rose-50);
    padding: 24px;
    display: grid;
    row-gap: 32px;
}

h1 {
    color: var(--rose-900);
    font-weight: var(--fw-bold);
    line-height: 120%;
    font-size: 40px;
}

div {
    display: grid;
    row-gap: 24px;
}
</style>
