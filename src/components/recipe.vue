<script setup>
import { computed } from "vue";

const props = defineProps(["image", "category", "name", "price"]);

const priceWithDecimal = computed(() => {
    return props.price.toFixed(2);
});
</script>

<template>
    <div class="recipe">
        <div class="recipeTop">
            <img :src="props.image" alt="recipe image" class="recipeImage" />
            <button type="button" class="addButton">
                <img src="/images/icon-add-to-cart.svg" alt="cart icon" />
                Add to cart
            </button>
        </div>
        <div class="recipeBottom">
            <span class="recipeCategory">{{ props.category }}</span>
            <p class="recipeName">{{ props.name }}</p>
            <p class="recipeTitle">${{ priceWithDecimal }}</p>
        </div>
    </div>
</template>

<style scoped>
.recipe {
    display: grid;
    row-gap: 16px;
}

.recipeTop {
    height: 234px;
    display: flex;
    justify-content: center;
    align-items: end;
    position: relative;
}

.recipeImage {
    height: 212px;
    margin-block-end: auto;
    border-radius: 8px;
}

.addButton {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    margin-inline: auto;
    max-width: fit-content;
    display: flex;
    gap: 8px;
    border-radius: 2rem;
    background-color: white;
    border: 1px solid var(--rose-400);
    padding-block: 12px;
    padding-inline: 24px;
    color: var(--rose-900);
    font-size: 14px;
    font-weight: var(--fw-semiBold);
}

.recipeBottom {
    display: grid;
    row-gap: 4px;
}

.recipeCategory {
    font-size: 14px;
    color: var(--rose-500);
}

.recipeName {
    font-size: var(--fs-body);
    font-weight: var(--fw-semiBold);
    color: var(--rose-900);
}

.recipeTitle {
    font-size: var(--fs-body);
    font-weight: var(--fw-semiBold);
    color: var(--red);
}
</style>
