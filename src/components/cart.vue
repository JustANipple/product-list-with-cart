<script setup>
import { computed } from "vue";

const props = defineProps(["cartList"]);
const emits = defineEmits(["remove-from-cart", "show-modal"]);

const totalPrice = computed(() =>
    props.cartList
        .reduce((partialSum, a) => partialSum + a.price * a.quantity, 0)
        .toFixed(2)
);

const totalQuantity = computed(() =>
    props.cartList.reduce((partialSum, a) => partialSum + a.quantity, 0)
);

const totalItems = computed(
    () => props.cartList.filter((item) => item.quantity > 0).length
);

function removeFromCart(name) {
    emits("remove-from-cart", name);
}

function showModal() {
    emits("show-modal");
}
</script>

<template>
    <div class="cart">
        <h2 class="textPresetTwo cartTitle">
            Your Cart ({{ totalQuantity ?? 0 }})
        </h2>
        <div class="cartEmpty" v-if="totalQuantity == 0">
            <img src="/images/illustration-empty-cart.svg" alt="a cake" />
            <p class="textPresetFourBold cartParagraph">
                Your added items will appear here
            </p>
        </div>
        <div v-else class="cartFull">
            <ul class="cartList">
                <li
                    v-for="(recipe, index) in props.cartList.filter(
                        (item) => item.quantity > 0
                    )"
                    :key="index"
                    class="cartRecipe"
                >
                    <div class="recipeContainer">
                        <div class="containerLeft">
                            <p class="textPresetFourBold recipeName">
                                {{ recipe.name }}
                            </p>
                            <div class="recipeInfo">
                                <p class="textPresetFourBold infoQuantity">
                                    {{ recipe.quantity }}x
                                </p>
                                <p class="textPresetFour singlePrice">
                                    @${{ recipe.price.toFixed(2) }}
                                </p>
                                <p class="textPresetFourBold quantityPrice">
                                    ${{
                                        (
                                            recipe.price * recipe.quantity
                                        ).toFixed(2)
                                    }}
                                </p>
                            </div>
                        </div>
                        <button
                            type="button"
                            class="containerRight"
                            @click="removeFromCart(recipe.name)"
                        >
                            <img
                                src="/images/icon-remove-item.svg"
                                alt="remove item"
                                class="removeItemIcon"
                            />
                        </button>
                    </div>
                    <div
                        v-show="index < totalItems - 1"
                        class="recipeDivisor"
                    ></div>
                </li>
            </ul>
            <div class="divisor"></div>
            <div class="orderTotal">
                <p class="textPresetFour totalText">Order Total</p>
                <p class="textPresetTwo totalPrice">${{ totalPrice }}</p>
            </div>
            <div class="carbonNeutral">
                <img
                    src="/images/icon-carbon-neutral.svg"
                    alt="carbon neutral"
                    class="carbonNeutralIcon"
                />
                <p class="textPresetFour carbonNeutralParagraph">
                    This is a
                    <span class="textPresetFourBold carbonNeutralParBold"
                        >carbon-neutral</span
                    >
                    delivery
                </p>
            </div>
            <button
                type="button"
                class="textPresetThree confirmButton"
                @click="showModal"
            >
                Confirm Order
            </button>
        </div>
    </div>
</template>

<style scoped>
.cart {
    padding: 24px;
    background-color: white;
    display: grid;
    row-gap: 24px;
    border-radius: 12px;
}

.cartTitle {
    color: var(--red);
}

.cartEmpty {
    padding-block: 16px;
    display: grid;
    place-items: center;
    row-gap: 16px;
}

.cartParagraph {
    color: var(--rose-500);
}

.cartFull {
    display: grid;
    row-gap: 24px;
}

.cartList {
    list-style-type: none;
    padding: unset;
    display: grid;
    row-gap: 16px;
}

.cartRecipe {
    display: grid;
    row-gap: 16px;
}

.recipeContainer {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.containerLeft {
    display: grid;
    row-gap: 5px;
}

.recipeName {
    color: var(--rose-900);
}

.recipeInfo {
    display: flex;
    gap: 8px;
}

.infoQuantity {
    color: var(--red);
}

.singlePrice {
    color: var(--rose-500);
}

.quantityPrice {
    color: var(--rose-500);
}

.containerRight {
    aspect-ratio: 1/1;
    width: 18px;
    border-radius: 2rem;
    border: 1px solid var(--rose-400);
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: transparent;
}

.recipeDivisor {
    border-block-start: 1px solid var(--rose-100);
}

.divisor {
    border-block-start: 1px solid var(--rose-100);
}

.orderTotal {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.totalText {
    color: var(--rose-900);
}

.totalPrice {
    color: var(--rose-900);
}

.carbonNeutral {
    display: flex;
    gap: 8px;
    justify-content: center;
    align-items: center;
    padding: 16px;
    border-radius: 8px;
    background-color: var(--rose-50);
}

.carbonNeutralParagraph {
    color: var(--rose-900);
}

.confirmButton {
    padding: 16px 24px;
    background-color: var(--red);
    border: unset;
    border-radius: 2rem;
    color: white;
}
</style>
