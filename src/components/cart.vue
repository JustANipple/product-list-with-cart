<script setup>
import { computed } from "vue";

const props = defineProps(["totalQuantity", "cartList"]);
const totalPrice = computed(() =>
    props.cartList.reduce(
        (partialSum, a) => partialSum + a.price * a.quantity,
        0
    )
);
</script>

<template>
    <div class="cart">
        <h2 class="textPresetTwo cartTitle">
            Your Cart ({{ props.totalQuantity ?? 0 }})
        </h2>
        <div class="cartEmpty" v-if="props.totalQuantity == 0">
            <img src="/images/illustration-empty-cart.svg" alt="a cake" />
            <p class="textPresetFourBold cartParagraph">
                Your added items will appear here
            </p>
        </div>
        <ul v-else class="cartFull">
            <li v-for="(recipe, index) in props.cartList" :key="index">
                <div>
                    <div>
                        {{ recipe.name }}
                        <div>
                            {{ recipe.quantity }}x
                            <div>
                                <p>@${{ recipe.price.toFixed(2) }}</p>
                                <p>
                                    ${{
                                        recipe.price.toFixed(2) *
                                        recipe.quantity
                                    }}
                                </p>
                            </div>
                        </div>
                    </div>
                    <img src="/images/icon-remove-item.svg" alt="remove item" />
                </div>
                <div v-if="index < props.cartList.length - 1"></div>
            </li>
        </ul>
        <div></div>
        <div>
            <p>Order total</p>
            <p>{{ totalPrice }}</p>
        </div>
        <div>
            <img src="/images/icon-carbon-neutral.svg" alt="carbon neutral" />
            <p>This is a <span>carbon-neutral</span> delivery</p>
        </div>
        <button>Confirm Order</button>
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
    row-gap: 16px;
}
</style>
