<script setup>
import jsonData from "./data.json";
import recipe from "./components/recipe.vue";
import cart from "./components/cart.vue";
import modal from "./components/modal.vue";

import { ref } from "vue";

const datas = jsonData;
const cartList = ref([]);
const isConfirmed = ref(false);
const windowWidth = ref(window.innerWidth);

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
    window.scrollTo({ top: 0, behavior: "smooth" });
    setTimeout(() => {
        document.querySelector("body").style.height = "100%";
        document.querySelector("body").style.overflow = "hidden";
    }, 800);
}

function hideModal() {
    cartList.value.forEach((item) => (item.quantity = 0));
    isConfirmed.value = false;
    document.querySelector("body").style.height = "100vh";
    document.querySelector("body").style.overflow = "unset";
}

function getRecipeImage(item) {
    if (windowWidth < 768) {
        return item.image.mobile;
    } else if (windowWidth < 1440) {
        return item.image.tablet;
    } else {
        return item.image.desktop;
    }
}
</script>

<template>
    <main class="desserts">
        <h1 class="textPresetOne mainTitle">Desserts</h1>
        <div class="recipeList">
            <recipe
                v-for="(item, index) in cartList"
                :image="getRecipeImage(item)"
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
    <main v-if="isConfirmed" class="modalContainer">
        <modal :cart-list="cartList" @hide-modal="hideModal" />
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

@media screen and (min-width: 768px) {
    .desserts {
        padding: 40px;
    }

    .recipeList {
        display: flex;
        flex-wrap: wrap;
        column-gap: 24px;
        row-gap: 32px;
    }
}

@media screen and (min-width: 1440px) {
    .desserts {
        padding-block: 88px;
        display: grid;
        place-content: center;
        grid-template-columns: repeat(12, 72px);
        gap: 32px;
    }

    .mainTitle {
        grid-row-start: 1;
        grid-row-end: 2;
        grid-column-start: 1;
        grid-column-end: 3;
    }

    .recipeList {
        grid-column-start: 1;
        grid-column-end: 9;
        grid-row-start: 2;
    }
}
</style>
