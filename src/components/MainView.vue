<template>
  <div class="section__wrapper">
    <div class="section__wrapper__content _container">
      <div class="section__wrapper__bill">
        <img
          src="@/assets/billgates.jpg"
          alt=""
          class="section__wrapper__bill__img"
        />

        <div class="section__wrapper__bill__title">Spend Bill Gates' Money</div>
      </div>
      <div class="section__wrapper__header">
        <h1 class="section__wrapper__header__total">
          <count-up :start-val="0" :end-val="billion - totalOfItems"></count-up>
        </h1>
      </div>
      <ItemsList
        :items="items"
        @decrease="decreaseCount"
        @increase="increaseCount"
      />

      <div class="section__wrapper__receipt" v-if="filteredItems.length > 0">
        <h2 class="section__wrapper__receipt__title">Your Receipt</h2>

        <div
          class="section__wrapper__receipt__item"
          v-for="item in filteredItems"
          :key="item.id"
        >
          <p class="section__wrapper__receipt__item__title">{{ item.title }}</p>
          <p class="section__wrapper__receipt__item__quantity">
            x{{ formattedQuantity(item.quantity) }}
          </p>
          <p class="section__wrapper__receipt__item__price">
            {{ formattedPrice(item.quantity, item.price) }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import ItemsList from "@/components/ItemsList.vue";
import { defineComponent, ref, computed } from "vue";
import { Item } from "@/types/Item";
import { items as defaultItems } from "@/types/List";
import CountUp from "vue-countup-v3";
export default defineComponent({
  name: "App",
  components: {
    ItemsList,
    CountUp,
  },
  setup() {
    const items = ref<Item[]>(defaultItems);

    const billion = 100000000000;

    const decreaseCount = (itemId: number) => {
      const id = findById(itemId);
      if (items.value[id].quantity > 0) {
        items.value[id].quantity -= 1;
      }
    };

    const increaseCount = (itemId: number) => {
      const id = findById(itemId);
      items.value[id].quantity += 1;
    };

    const findById = (itemId: number) => {
      return items.value.findIndex((item) => item.id === itemId);
    };

    const formatNumber = (value: number) => {
      if (value < 1000) {
        return value.toString();
      } else if (value < 1000000) {
        return `${(value / 1000).toFixed(1)}K`;
      } else if (value < 1000000000) {
        return `${(value / 1000000).toFixed(1)}M`;
      } else {
        return `${(value / 1000000000).toFixed(1)}B`;
      }
    };

    const formattedPrice = (quantity: number, price: number) => {
      const total = quantity * price;
      return `$${formatNumber(total)}`;
    };

    const formattedQuantity = (quantity: number) => {
      return formatNumber(quantity);
    };

    // Computed property for calculating the total
    const totalOfItems = computed(() => {
      return items.value.reduce((acc, item) => {
        return acc + item.quantity * item.price;
      }, 0);
    });

    // Computed property for filtering items with quantity greater than zero
    const filteredItems = computed(() => {
      return items.value.filter((item) => item.quantity > 0);
    });

    return {
      items,
      billion,
      totalOfItems,
      filteredItems,
      decreaseCount,
      increaseCount,
      formatNumber,
      formattedPrice,
      formattedQuantity,
    };
  },
});
</script>
