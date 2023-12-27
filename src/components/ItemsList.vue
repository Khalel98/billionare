<template>
  <div class="section__list">
    <div
      class="section__list__item"
      v-for="(item, index) in items"
      :key="index"
    >
      <img
        :src="require(`@/assets/images/${item.img}`)"
        alt=""
        class="section__list__item__img"
      />
      <div class="section__list__item__title">{{ item.title }}</div>
      <div class="section__list__item__price">${{ item.price }}</div>
      <div class="section__list__item__action">
        <button
          class="section__list__item__sell _btn"
          :class="{ active: item.quantity > 0 }"
          @click="$emit('decrease', item.id)"
        >
          Sell
        </button>

        <input
          type="text"
          class="section__list__item__quantity"
          v-model="item.quantity"
        />
        <button
          class="section__list__item__buy _btn"
          @click="$emit('increase', item.id)"
        >
          Buy
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import { Item } from "@/types/Item";

export default defineComponent({
  emits: ["decrease", "increase"],
  props: {
    items: {
      required: true,
      type: Array as PropType<Item[]>,
    },
  },
  setup() {
    return {};
  },
});
</script>
<style lang="scss"></style>
