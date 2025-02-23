<script setup>
import { ref, computed } from "vue";

const props = defineProps(["image", "category", "name", "price", "quantity"]);
const emit = defineEmits(["add-to-cart", "remove-from-cart"]);

const priceWithDecimal = computed(() => {
    return props.price.toFixed(2);
});

const isInCart = computed(() => props.quantity > 0);

function addToCart() {
    emit("add-to-cart");
}

function removeFromCart() {
    emit("remove-from-cart");
}
</script>

<template>
    <div class="recipe">
        <div class="recipeTop">
            <img
                :src="props.image"
                alt="recipe image"
                class="recipeImage"
                :class="{ isBordered: isInCart }"
            />
            <button
                type="button"
                class="textPresetFourBold addButton"
                @click="addToCart"
                v-if="props.quantity === 0"
            >
                <img src="/images/icon-add-to-cart.svg" alt="cart icon" />
                Add to Cart
            </button>
            <button type="button" class="textPresetFourBold editButton" v-else>
                <div @click="removeFromCart" class="decrementIconContainer">
                    <img
                        src="/images/icon-decrement-quantity.svg"
                        alt="decrement icon"
                    />
                </div>
                {{ props.quantity }}
                <div @click="addToCart" class="incrementIconContainer">
                    <img
                        src="/images/icon-increment-quantity.svg"
                        alt="increment icon"
                    />
                </div>
            </button>
        </div>
        <div class="recipeBottom">
            <span class="textPresetFour recipeCategory">{{
                props.category
            }}</span>
            <p class="textPresetThree recipeName">{{ props.name }}</p>
            <p class="textPresetThree recipeTitle">${{ priceWithDecimal }}</p>
        </div>
    </div>
</template>

<style scoped>
.recipe {
    display: grid;
    row-gap: 16px;
    max-width: fit-content;
}

.recipeTop {
    position: relative;
    z-index: 0;
}

.recipeImage {
    height: 212px;
    margin-block-end: auto;
    border-radius: 8px;
    position: relative;
    z-index: -1;
}

.isBordered {
    border: 2px solid var(--red);
}

.addButton {
    margin-inline: auto;
    max-width: fit-content;
    display: flex;
    gap: 8px;
    border-radius: 2rem;
    background-color: white;
    border: 1px solid var(--rose-400);
    padding-block: 10px;
    padding-inline: 26px;
    color: var(--rose-900);
    margin-block-start: -22px;
}

.editButton {
    width: 160px;
    background-color: var(--red);
    padding-block: 11px;
    padding-inline: 12px;
    border-radius: 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border: unset;
    margin-inline: auto;
    margin-block-start: -22px;
    color: white;
}

.editButton div {
    border: 1px solid white;
    border-radius: 50%;
    aspect-ratio: 1/1;
    width: 18px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.recipeBottom {
    display: grid;
    row-gap: 1.25px;
}

.recipeCategory {
    color: var(--rose-500);
}

.recipeName {
    color: var(--rose-900);
}

.recipeTitle {
    color: var(--red);
}

@media screen and (min-width: 768px) {
    .recipe {
        flex: 1 1 calc(33.33% - 24px);
    }
}

@media screen and (min-width: 1440px) {
    .recipeImage {
        height: 240px;
    }

    .addButton {
        transition: all 0.125s ease-in-out;
    }

    .addButton:hover {
        cursor: pointer;
        border-color: var(--red);
        color: var(--red);
    }

    .decrementIconContainer,
    .incrementIconContainer {
        transition: all 0.125s ease-in-out;
    }

    .decrementIconContainer:hover,
    .incrementIconContainer:hover {
        cursor: pointer;
        background-color: #952c0b;
    }
}
</style>
