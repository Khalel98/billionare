<!--Child component-->
<template>
  <div class="item__body">
   <div class="item__body__content">
      <img  :src="resolve_img_url(picture_src)" alt="" class="item__body__content__img">
      <!--<p>{{ this.totalOfItem }}</p>-->
      <p class="item__body__content__title">{{ this.title }}</p>
      <p class="item__body__content__price">${{ this.price }}</p>
      <div class="item__body__content__control">
         <button class="item__body__content__btn sell" @click="count--">Sell</button>
         <input type="text" class="item__body__content__input" :value=this.count @input="nullCount" @keypress='onlyNumber(event)'>
         <button class="item__body__content__btn buy" @click="count++">Buy</button>
      </div>
   </div>
   <div class="info">
      <p>{{this.info_title }}</p>
      <p>{{this.info_count }}</p>
      <p>{{this.info_totalOfItem}}</p>
   </div>
   
  </div>
</template>

<script>

export default {
   inherit: true,
   props: {
    title: String,
    price: Number,    
    picture_src: String,

  },
  data(){
   return{
      count:0,
      totalOfItem: 0,
      info_title: '',
      info_count: '',
      info_totalOfItem: ''
   }
   },
   methods:{
      resolve_img_url: function (path) {
      let images = require.context('../assets/images/', false, /\.png$|\.jpg$/)
      return images("./"+path)
    },
    nullCount(event){
      this.count = event.target.value
    },
    onlyNumber(evt) {
		var theEvent = evt || window.event;

		// Handle paste
		if (theEvent.type === 'paste') {
				key = event.clipboardData.getData('text/plain');
		} else {
		// Handle key press
				var key = theEvent.keyCode || theEvent.which;
				key = String.fromCharCode(key);
		}
		var regex = /[0-9]|\./;
		if( !regex.test(key) ) {
			theEvent.returnValue = false;
			if(theEvent.preventDefault) theEvent.preventDefault();
		}
		},
   },
   watch: {
      count(val) {
         this.totalOfItem = val * this.price;
         if(val > 0){
            this.info_title = this.title
            this.info_count ='x' +  this.count
            this.info_totalOfItem ='$'+ this.totalOfItem
         }else{
            this.info_title = ' '
            this.info_count = ' '
            this.info_totalOfItem = ' '

         }
      },
      totalOfItem(val, oldVal) {
         this.$emit('clicked', val - oldVal);
      },
   },
}
</script>

<style>
.item__body{
   margin-top: 7px;
   background: #fff;
   padding: 20px;
}
.item__body__content__title{
   font-size: 22px;
   font-weight: 700;
}

.item__body__content__price{
    font-size: 20px;
    color: #24c486;
}

img{
   height: 100px;
}
.item__body__content__control{
   width: 100%;
   display: flex;
   justify-content: space-between;
}

.item__body__content__btn{
   background: none;
    border: none;
    color: #333;
    cursor: auto;
    touch-action: manipulation;
    cursor: pointer;
    padding: 10px 12px;
    border-radius: 3px;
    color: #fff;
    border: none;
    font-size: 16px;
    font-weight: 700;
    text-align: center;
    width: 100%; 
}

.sell{
   background: linear-gradient(180deg,#f53b82,#f53b57);
}
.buy{
   background: linear-gradient(180deg,#2ecc71,#1abc9c);
}

.item__body__content__input{
   margin: 0 10px;
   width: 100px;
   font-size: 16px;
   text-align: center;
}

.info{
   display: none;
}
</style>