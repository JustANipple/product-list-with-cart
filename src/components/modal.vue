<script setup>
import { computed } from "vue";

const props = defineProps(["cartList"]);
const cartItems = computed(() =>
    props.cartList.filter((item) => item.quantity > 0)
);
</script>

<template>
    <div class="modal">
        <div class="header">
            <img
                src="/images/icon-order-confirmed.svg"
                alt="check icon"
                class="checkIcon"
            />
            <p class="title">Order Confirmed</p>
            <p class="subtitle">We hope you enjoy your food!</p>
        </div>
        <div class="orderContainer">
            <ul class="recipeList">
                <li
                    v-for="(item, index) in cartItems"
                    :key="index"
                    class="recipeRow"
                >
                    <div class="rowLeft">
                        <img :src="item.image.mobile" alt="recipe image" />
                        <div class="recipeRowInfo">
                            <p class="recipeName">{{ item.name }}</p>
                            <div class="recipePricePerQuantity">
                                <p>{{ item.quantity }}</p>
                                <p>@${{ item.price }}</p>
                            </div>
                        </div>
                    </div>
                    <p class="recipePrice">
                        {{ `$${(item.price * item.quantity).toFixed(2)}` }}
                    </p>
                </li>
                <div v-show="index < cartItems.length - 2">Ciao</div>
            </ul>
        </div>
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
</style>
