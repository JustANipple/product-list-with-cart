<script setup>
import jsonData from "./data.json";
import recipe from "./components/recipe.vue";
import cart from "./components/cart.vue";
import modal from "./components/modal.vue";

import { ref } from "vue";

const datas = jsonData;
const cartList = ref([]);
const isConfirmed = ref(false);

for (const data of datas) {
    const recipe = {
        image: data.image,
        name: data.name,
        category: data.category,
        price: data.price,
        quantity: 0,
    };

    cartList.value.push(recipe);
}

function addToCart(name) {
    cartList.value.find((item) => item.name === name).quantity++;
}

function removeFromCart(name) {
    cartList.value.find((item) => item.name === name).quantity--;
}

function showModal() {
    isConfirmed.value = true;
    console.log(isConfirmed.value);
}
</script>

<template>
    <main class="desserts">
        <h1 class="textPresetOne mainTitle">Desserts</h1>
        {{ isConfirmed }}
        <div class="recipeList">
            <recipe
                v-for="(item, index) in cartList"
                :image="item.image.mobile"
                :category="item.category"
                :name="item.name"
                :price="item.price"
                :quantity="item.quantity"
                :key="index"
                @add-to-cart="addToCart(item.name)"
                @remove-from-cart="removeFromCart(item.name)"
            />
        </div>
        <cart
            :cart-list="cartList"
            @remove-from-cart="removeFromCart"
            @show-modal="showModal"
        />
    </main>
    <main v-show="isConfirmed" class="modalContainer">
        <modal :cart-list="cartList" />
    </main>
</template>

<style scoped>
.desserts {
    background-color: var(--rose-50);
    padding: 24px;
    display: grid;
    row-gap: 32px;
}

.mainTitle {
    color: var(--rose-900);
}

.recipeList {
    display: grid;
    row-gap: 22.5px;
    place-content: center;
}

.modalContainer {
    background-color: hsla(0, 0%, 0%, 0.5);
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    display: flex;
    align-items: flex-end;
}
</style>
