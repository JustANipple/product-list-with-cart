<script setup>
import jsonData from "./data.json";
import recipe from "./components/recipe.vue";
import cart from "./components/cart.vue";

import { ref, computed } from "vue";

const datas = jsonData;

const cartList = ref([]);
const cartLength = computed(() => cartList.value.length);

function updateCart(index) {
    const itemToAdd = datas[index];
    const existingItem = cartList.value.find(
        (item) => item.name === itemToAdd.name
    );

    if (existingItem) {
        existingItem.quantity++;
    } else {
        cartList.value.push({ ...itemToAdd, quantity: 1 });
    }
}

function removeFromCart(index) {
    const itemToRemove = datas[index];
    const existingItem = cartList.value.find(
        (item) => item.name === itemToRemove.name
    );

    if (existingItem) {
        if (existingItem.quantity > 1) {
            existingItem.quantity--;
        } else {
            const itemIndex = cartList.value.indexOf(existingItem);
            if (itemIndex !== -1) {
                cartList.value.splice(itemIndex, 1);
            }
        }
    }
}
</script>

<template>
    <main>
        <h1 class="textPresetOne mainTitle">Desserts</h1>
        <div class="recipeList">
            <recipe
                v-for="(data, index) in datas"
                :image="data.image.mobile"
                :category="data.category"
                :name="data.name"
                :price="data.price"
                :key="index"
                @add-to-cart="updateCart(index)"
                @remove-from-cart="removeFromCart(index)"
            />
        </div>
        <cart :total-quantity="cartLength" :cart-list="cartList" />
    </main>
</template>

<style scoped>
main {
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
</style>
