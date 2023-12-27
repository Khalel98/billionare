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
          $ {{ billion - totalOfItems }}
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

export default defineComponent({
  name: "App",
  components: {
    ItemsList,
  },
  setup() {
    const items = ref<Item[]>([
      { id: 1, quantity: 0, title: "Big Mac", price: 2, img: "big-mac.jpg" },
      {
        id: 2,
        quantity: 0,
        title: "Flip Flops",
        price: 3,
        img: "flip-flops.jpg",
      },
      {
        id: 3,
        quantity: 0,
        title: "Coca-Cola Pack",
        price: 5,
        img: "coca-cola-pack.jpg",
      },
      {
        id: 4,
        quantity: 0,
        title: "Movie Ticket",
        price: 12,
        img: "movie-ticket.jpg",
      },
      { id: 5, quantity: 0, title: "Book", price: 15, img: "book.jpg" },
      {
        id: 6,
        quantity: 0,
        title: "Lobster Dinner",
        price: 45,
        img: "lobster-dinner.jpg",
      },
      {
        id: 7,
        quantity: 0,
        title: "Video Game",
        price: 60,
        img: "video-game.jpg",
      },
      {
        id: 8,
        quantity: 0,
        title: "Amazon Echo",
        price: 99,
        img: "amazon-echo.jpg",
      },
      {
        id: 9,
        quantity: 0,
        title: "Year of Netflix",
        price: 100,
        img: "year-of-netflix.jpg",
      },
      {
        id: 10,
        quantity: 0,
        title: "Air Jordans",
        price: 125,
        img: "air-jordans.jpg",
      },
      { id: 11, quantity: 0, title: "Airpods", price: 199, img: "airpods.jpg" },
      {
        id: 12,
        quantity: 0,
        title: "Gaming Console",
        price: 299,
        img: "gaming-console.jpg",
      },

      {
        id: 13,
        quantity: 0,
        title: "Drone",
        price: 350,
        img: "drone.jpg",
      },

      {
        id: 14,
        quantity: 0,
        title: "Smartphone",
        price: 699,
        img: "smartphone.jpg",
      },

      {
        id: 15,
        quantity: 0,
        title: "Bike",
        price: 800,
        img: "bike.jpg",
      },

      {
        id: 16,
        quantity: 0,
        title: "Kitten",
        price: 1500,
        img: "kitten.jpg",
      },

      {
        id: 17,
        quantity: 0,
        title: "Puppy",
        price: 1500,
        img: "puppy.jpg",
      },

      {
        id: 18,
        quantity: 0,
        title: "Auto Rickshaw",
        price: 2300,
        img: "auto-rickshaw.jpg",
      },
      {
        id: 19,
        quantity: 0,
        title: "Horse",
        price: 2500,
        img: "horse.jpg",
      },
      {
        id: 20,
        quantity: 0,
        title: "Acre of Farmland",
        price: 3000,
        img: "acre-of-farmland.jpg",
      },

      {
        id: 21,
        quantity: 0,
        title: "Designer Handbag",
        price: 5500,
        img: "designer-handbag.jpg",
      },

      {
        id: 22,
        quantity: 0,
        title: "Hot Tub",
        price: 5000,
        img: "hot-tub.jpg",
      },

      {
        id: 23,
        quantity: 0,
        title: "Luxury Wine",
        price: 7000,
        img: "luxury-wine.jpg",
      },

      {
        id: 24,
        quantity: 0,
        title: "Diamond Ring",
        price: 10000,
        img: "diamond-ring.jpg",
      },

      {
        id: 25,
        quantity: 0,
        title: "Jet Ski",
        price: 12000,
        img: "jet-ski.jpg",
      },
      {
        id: 26,
        quantity: 0,
        title: "Rolex",
        price: 15000,
        img: "rolex.jpg",
      },
      {
        id: 27,
        quantity: 0,
        title: "Ford F-150",
        price: 30000,
        img: "ford-f-150.jpg",
      },
      {
        id: 28,
        quantity: 0,
        title: "Tesla",
        price: 75000,
        img: "tesla.jpg",
      },
      {
        id: 29,
        quantity: 0,
        title: "Monster Truck",
        price: 150000,
        img: "monster-truck.jpg",
      },
      {
        id: 30,
        quantity: 0,
        title: "Ferrari",
        price: 250000,
        img: "ferrari.jpg",
      },
      {
        id: 31,
        quantity: 0,
        title: "Single Family Home",
        price: 300000,
        img: "single-family-home.jpg",
      },

      {
        id: 32,
        quantity: 0,
        title: "Gold Bar",
        price: 700000,
        img: "gold-bar.jpg",
      },

      {
        id: 33,
        quantity: 0,
        title: "McDonalds Franchise",
        price: 1500,
        img: "mcdonalds-franchise.jpg",
      },

      {
        id: 34,
        quantity: 0,
        title: "Superbowl Ad",
        price: 5250000,
        img: "superbowl-ad.jpg",
      },

      {
        id: 35,
        quantity: 0,
        title: "Yacht",
        price: 7500000,
        img: "yacht.jpg",
      },

      {
        id: 36,
        quantity: 0,
        title: "M1 Abrams",
        price: 8000000,
        img: "m1-abrams.jpg",
      },

      {
        id: 37,
        quantity: 0,
        title: "Formula 1 Car",
        price: 15000000,
        img: "formula-1-car.jpg",
      },

      {
        id: 38,
        quantity: 0,
        title: "Apache Helicopter",
        price: 31000000,
        img: "apache-helicopter.jpg",
      },

      {
        id: 39,
        quantity: 0,
        title: "Mansion",
        price: 45000000,
        img: "mansion.jpg",
      },

      {
        id: 40,
        quantity: 0,
        title: "Make a Movie",
        price: 10000000,
        img: "make-a-movie.jpg",
      },

      {
        id: 41,
        quantity: 0,
        title: "Boeing 747",
        price: 14800000,
        img: "boeing-747.jpg",
      },

      {
        id: 42,
        quantity: 0,
        title: "Mona Lisa",
        price: 78000000,
        img: "mona-lisa.jpg",
      },

      {
        id: 43,
        quantity: 0,
        title: "Skyscraper",
        price: 850000000,
        img: "skyscraper.jpg",
      },

      {
        id: 44,
        quantity: 0,
        title: "Cruise Ship",
        price: 930000000,
        img: "cruise-ship.jpg",
      },

      {
        id: 45,
        quantity: 0,
        title: "NBA Team",
        price: 2120000000,
        img: "nba-team.jpg",
      },
    ]);

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

    const formattedPrice = (quantity: number, price: number) => {
      const total = quantity * price;

      if (total < 1000) {
        return `$${total}`;
      } else if (total < 1000000) {
        return `$${(total / 1000).toFixed(1)}K`;
      } else if (total < 1000000000) {
        return `$${(total / 1000000).toFixed(1)}M`;
      } else {
        return `$${(total / 1000000000).toFixed(1)}B`;
      }
    };

    const formattedQuantity = (quantity: number) => {
      const total = quantity;

      if (total < 1000) {
        return `${total}`;
      } else if (total < 1000000) {
        return `${(total / 1000).toFixed(1)}K`;
      } else if (total < 1000000000) {
        return `${(total / 1000000).toFixed(1)}M`;
      } else {
        return `${(total / 1000000000).toFixed(1)}B`;
      }
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
      formattedPrice,
      formattedQuantity,
    };
  },
});
</script>
