<script setup>
import { computed } from "vue";

const props = defineProps(["cartList"]);
const emits = defineEmits(["hide-modal"]);
const cartItems = computed(() =>
    props.cartList.filter((item) => item.quantity > 0)
);
const orderTotalPrice = computed(() =>
    props.cartList.reduce(
        (accumulator, currentValue) =>
            accumulator + currentValue.price * currentValue.quantity,
        0
    )
);

function hideModal() {
    emits("hide-modal");
}
</script>

<template>
    <div class="modal">
        <div class="titleInfo">
            <img
                src="/images/icon-order-confirmed.svg"
                alt="check icon"
                class="checkIcon"
            />
            <div class="textContainer">
                <p class="textPresetOne title">Order Confirmed</p>
                <p class="subtitle">We hope you enjoy your food!</p>
            </div>
        </div>
        <div class="orderContainer">
            <ul class="confirmedItems">
                <li
                    v-for="(item, index) in cartItems"
                    :key="index"
                    class="recipeRow"
                >
                    <div class="rowContainer">
                        <div class="rowLeft">
                            <img
                                :src="item.image.thumbnail"
                                alt="recipe image"
                                class="recipeImage"
                            />
                            <div class="recipeRowInfo">
                                <p class="textPresetFourBold recipeName">
                                    {{ item.name }}
                                </p>
                                <div class="recipePricePerQuantity">
                                    <p
                                        class="textPresetFourBold recipeQuantity"
                                    >
                                        {{ item.quantity }}x
                                    </p>
                                    <p class="textPresetFour recipeSinglePrice">
                                        {{ `@$${item.price.toFixed(2)}` }}
                                    </p>
                                </div>
                            </div>
                        </div>
                        <p class="textPresetThree recipeTotalPrice">
                            {{ `$${(item.price * item.quantity).toFixed(2)}` }}
                        </p>
                    </div>
                    <div
                        v-show="index < cartItems.length - 1"
                        class="itemSeparator"
                    ></div>
                </li>
            </ul>
            <div class="orderSeparator"></div>
            <div class="orderTotal">
                <p class="textPresetFour ordetTotalText">Order Total</p>
                <p class="textPresetTwo orderTotalPrice">
                    {{ `$${orderTotalPrice.toFixed(2)}` }}
                </p>
            </div>
        </div>
        <button
            type="button"
            class="textPresetThree restartButton"
            @click="hideModal"
        >
            Start New Order
        </button>
    </div>
</template>

<style scoped>
.modal {
    background-color: white;
    margin-block-start: auto;
    border-top-left-radius: 12px;
    border-top-right-radius: 12px;
    padding: 24px;
    padding-top: 40px;
    width: 100%;
    display: grid;
    row-gap: 32px;
}

.titleInfo {
    display: grid;
    row-gap: 24px;
}

.textContainer {
    display: grid;
    row-gap: 8px;
}

.title {
    color: var(--rose-900);
}

.subtitle {
    color: var(--rose-500);
}

.orderContainer {
    background-color: var(--rose-50);
    padding: 24px;
    border-radius: 8px;
    display: grid;
    row-gap: 24px;
}

.confirmedItems {
    display: grid;
    row-gap: 16px;
    padding: unset;
}

.recipeRow {
    display: grid;
    row-gap: 16px;
}

.rowContainer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 8px;
}

.rowLeft {
    display: flex;
    gap: 16px;
}

.recipeImage {
    aspect-ratio: 1/1;
    height: 48px;
    border-radius: 4px;
}

.recipeRowInfo {
    display: grid;
    row-gap: 8px;
}

.recipeName {
    color: var(--rose-900);
}

.recipePricePerQuantity {
    display: flex;
    gap: 8px;
}

.recipeQuantity {
    color: var(--red);
}

.recipeSinglePrice {
    color: var(--rose-500);
}

.recipeTotalPrice {
    color: var(--rose-900);
}

.itemSeparator {
    border-top: 1px solid var(--rose-100);
}

.orderSeparator {
    border-top: 1px solid var(--rose-100);
}

.orderTotal {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.ordetTotalText {
    color: var(--rose-900);
}

.orderTotalPrice {
    color: var(--rose-900);
}

.restartButton {
    background-color: var(--red);
    border: unset;
    border-radius: 2rem;
    color: white;
    padding: 16px 24px;
}

@media screen and (min-width: 768px) {
    .modal {
        padding: 40px;
        margin-block-start: unset;
        margin-inline: auto;
        border-radius: 12px;
        max-width: 592px;
    }
}
</style>
