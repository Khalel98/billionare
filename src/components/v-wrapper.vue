<!--Parent Component-->
<template>
  <div class="section__wrapper">
    <h1 class="section_total">{{ this.total }}</h1>
    <div class="container">
      <div class="row">
        <div class="input-container" v-for="field in fields" :key="field.title">
          <vItem
            :title="field.title"
            :price="field.price"
            :picture_src="field.img"
            @clicked="onClickChild"
          ></vItem>
        </div>
      </div>
    </div>
    <div class="receipt__body" v-show="open">
      <h2>Your Receipt</h2>
      <div id="receipt"></div>
      <hr />
      <h3>Total: ${{ 100000000000 - this.total }}</h3>
    </div>
  </div>
</template>

<script>
import vItem from "./v-item.vue";

export default {
  data() {
    return {
      total: 100000000000,
      infoParent: "",
      open: false,
      fields: [
        { title: "Big Mac", price: 2, img: "big-mac.jpg" },
        { title: "Flip Flops", price: 3, img: "flip-flops.jpg" },
        { title: "Coca-Cola Pack", price: 5, img: "coca-cola-pack.jpg" },
        { title: "Movie Ticket", price: 12, img: "movie-ticket.jpg" },
        { title: "Book", price: 15, img: "book.jpg" },
        { title: "Lobster Dinner", price: 45, img: "lobster-dinner.jpg" },
        { title: "Video Game", price: 60, img: "video-game.jpg" },
        { title: "Amazon Echo", price: 99, img: "amazon-echo.jpg" },
        { title: "Year of Netflix", price: 100, img: "year-of-netflix.jpg" },
        { title: "Air Jordans", price: 125, img: "air-jordans.jpg" },
        { title: "Airpods", price: 199, img: "airpods.jpg" },
        { title: "Mansion", price: 45000000, img: "mansion.jpg" },
      ],
    };
  },
  components: {
    vItem,
  },
  methods: {
    onClickChild(value) {
      this.total -= value;
      setTimeout(this.infoParentEach, 500);
    },
    infoParentEach() {
      let receipt = document.getElementById("receipt");
      receipt.innerHTML = "";
      let infoparent = document.getElementsByClassName("info");
      for (var index = 0; index < infoparent.length; index++) {
        if (
          infoparent[index].innerHTML == "<p></p><p></p><p></p>" ||
          infoparent[index].innerHTML == "<p> </p><p> </p><p> </p>"
        ) {
        } else {
          this.open = true;
          receipt.innerHTML +=
            '<span class="info_content">' +
            infoparent[index].innerHTML +
            "</span>";
        }
      }
    },
  },
};
</script>

<style>
body {
  background: #f1f2f6;
}
.section__wrapper {
  background: #f1f2f6;
  /*padding: 100px;  */
  max-width: 1000px;
  margin: 0 auto;
}
.section_total {
  color: #fff;
  background-color: #2ecc71;
  background: linear-gradient(180deg, #2ecc71, #1abc9c);
  padding: 20px;
  margin: 10px 0;
  font-family: Roboto, sans-serif;
  font-size: 32px;
  font-weight: 700;
  text-align: center;
  top: 0;
  position: sticky;
  z-index: 9999;
}
.row {
  width: 100%;
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}
.input-container {
  width: 30%;
}

@media only screen and (max-width: 1024px) {
  .input-container {
    width: 45%;
  }
}

@media only screen and (max-width: 768px) {
  .input-container {
    width: 100%;
  }
}
.receipt__body {
  margin-top: 30px;
  background: #fff;
  padding: 20px;
}
#receipt {
  display: flex;
  flex-direction: column;
  max-width: 400px;
  margin: 0 auto;
}

.info_content {
  display: flex;
  justify-content: space-around;
  text-align: left;
}
.info_content p {
  margin: 0;
  font-size: 22px;
  font-weight: 700;
  margin-top: 10px;
}
.info_content p:nth-child(1) {
  width: 60%;
}
.info_content p:nth-child(2) {
  width: 20%;
}
.info_content p:nth-child(3) {
  width: 20%;
  color: #24c486;
  text-align: right;
}
</style>
