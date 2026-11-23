<script setup>
import { ref, reactive, computed, watch } from "vue";

let data = reactive({
  product_name: "Smart Watch",
  price: 500000,
  availability: true,
  cart: 0,
  stock: 10,
  qty: 1,
  imgSource: "https://i.ibb.co/6ZbsrQF/sw-blue.jpg",
  altText: "Blue Color",
  colors: ["Blue", "Orange", "Green"],
  packagings: ["Bubble wrap", "Wood", "No Packaging"]
});

const negara=["Indonesia", "Konoha", "Sawit"]

const wa = "6282145830080";

function addToCart() {
  data.cart = data.cart + data.qty;
}

function qtyPlus() {
  if (data.qty < data.stock) {
    data.qty += 1;
  } else {
    alert("stock habis gabisa pesan");
  }
}
function qtyMin() {
  if (data.qty > 0) {
    data.qty -= 1;
  }
}

const remainingStock = computed(() => {
  return data.stock - data.qty;
});

function sisaStock() {
  return data.stock - data.qty;
}

const sisa = () => data.stock - data.qty;

function buyNow() {
  window.location.href = `https://wa.me/${wa}?text=Hallo%2C%20Saya%20ingin%20memesan%20%0AProduk%3A%20 ${data.product_name} %0AVariant%3A%20  ${data.choosenColor}  %0AJumlah%3A%20  ${data.qty}  %0A%0ATerimakasih`;
}

</script>

<template>
  <div id="product">
    <header>
      <h1>Electronic Store</h1>
      <p>Cart({{ data.cart }})</p>
    </header>
    
    <div class="product">
      <div class="pict">
        <!-- Code image source and alt binding here -->
        <img :src="data.imgSource" :alt="data.altText" id="product-pict" />
      </div>
      
      <div class="info">
        <h1>{{ data.product_name }}</h1>
        <div>
        <!-- for(let i = 0; i<10 ; i++ {}) -->
        <ul >
          <li v-for="(item, index) in negara" :key="index">{{ item }}</li>
        </ul>
      </div>

        <h2 style="text-decoration: line-through; color: gray">
          Rp{{ data.price }}
        </h2>
        <h2 style="color: green">Rp{{ data.price / 2 }}</h2>

        <h3 :style="{ color: data.availability ? 'green' : 'red' }">
          {{ data.availability ? "Available" : "Sold Out" }}
        </h3>
        <p>stock : {{ data.stock }}</p>
        <h3 v-if="data.stock > 3">Available</h3>
        <h3 v-else-if="data.stock > 0">Stock Menipis</h3>
        <h3 v-else>Out Of Stock</h3>

        <hr size="3" width="20%" color="black" align="left" />
        <div class="color-box">
          <h3>Choose Color:</h3>
          <!-- Code value binding and show radio button text here -->
          <span class="radio" v-for="(color, index) in data.colors">
            <input
              type="radio"
              name="color"
              :id=" 'color-' + index"
              :value="color"
            />{{ color }}</span>
        </div>
        <div class="color-box">
          <h3>Choose Packaging:</h3>
          <!-- Code value binding and show radio button text here -->
          <span class="radio" v-for="(packaging, index) in data.packagings" :key="index">
            <input
              type="radio"
              name="color"
              :id=" 'package-' + index"
              :value="packaging"
            />{{ packaging }}</span>
        </div>
        <div class="stock">
          <h3>Stock :</h3>
          <p v-if="data.stock - data.qty > 6" style="color: green">
            <b>Available </b> {{ remainingStock }}
          </p>
          <!-- Code second condition here -->
          <p v-else-if="data.stock - data.qty > 0" style="color: orange">
            <b>Stock Menipis </b> {{ remainingStock }}
          </p>
          <!-- Code else condition here -->
          <p v-else style="color: red">
            <b>Out of stock </b> {{ remainingStock }}
          </p>
        </div>

        <div class="qty">
          <h3>Masukkan Jumlah :</h3>
          <button @click="qtyMin" @keydown.down="qtyMin" id="qty_min">-</button>
          <input type="text" id="qty" v-model.number="data.qty" />
          <!-- bisa di disabled-->
          <button @click="qtyPlus" @keydown.up="qtyPlus" id="qty_plus">
            +
          </button>
        </div>

        <div>
          <p>Subtotal : Rp. {{ (data.price / 2) * data.qty }}</p>
        </div>

        <div class="button-product">
          <button
            type="button"
            id="cart"
            @click="addToCart"
            style="cursor: pointer"
          >
            Add To Cart
          </button>
          <!-- Code href binding here -->
          <button
            :class="{
              buyButton: data.availability,
              disabledButton: !data.availability,
            }"
            @click="buyNow"
          >
            Buy Now
          </button>
        </div>
        <h3>Detail :</h3>
        <div class="detail">
          <li>Smart</li>
          <li>Cute</li>
          <li>Lovable</li>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.product {
  display: flex;
  /* padding-top: 50px; */
}
.Available {
  color: green;
}

.Sold-Out {
  color: red;
}

img {
  width: 60%;
  padding-left: 60px;
  padding-top: 25px;
}

.pict {
  width: 40%;
}

.info {
  width: 60%;
  font-family: "Calibri";
}

h1 {
  font-size: 50px;
}

h2 {
  color: green;
}

.color-box,
.stock {
  display: flex;
}

.qty {
  display: flex;
  margin-bottom: 10px;
}

#qty {
  width: 30px;
  height: 30px;
  text-align: center;
  margin-top: -4px;
}

#qty_min {
  height: 30px;
  width: 30px;
  background-color: #ff4949;
  border: #289672;
  border-radius: 5px;
  margin-right: 5px;
}

#qty_plus {
  height: 30px;
  width: 30px;
  background-color: #29bb89;
  border: #c10000 solid 2px;
  border-radius: 5px;
  margin-left: 5px;
}

.radio,
#stock {
  margin-top: 21px;
  margin-left: 10px;
}

.detail {
  margin-left: 40px;
  /* margin-top: 10px; */
}

#cart {
  height: 40px;
  background-color: black;
  color: white;
  border: none;
  margin-right: 10px;
}

#buy {
  /* height: 40px; */
  width: 75px;
  padding-top: 6px;
  background-color: white;
  color: black;
  border: 3px solid black;
}

a {
  text-decoration: none;
  margin-left: 7px;
}

.button-product {
  margin-top: 30px;
  display: flex;
}

header {
  background-color: white;
  color: black;
  margin: auto -5px 10px -5px;
  height: 60px;
  border-bottom: 1px solid gray;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  display: flex;
}

header h1 {
  margin-left: 70px;
  font-size: 45px;
  margin-top: 0px;
}

header p {
  border: 2px solid black;
  padding-right: 10px;
  padding-left: 10px;
  padding-top: 5px;
  margin-left: 700px;
  height: 25px;
}

.buyButton {
  color: black;
  background-color: white;
  width: 75px;
  height: 28px;
  text-align: center;
  padding-top: 6px;
  border: 3px solid black;
}

.disabledButton {
  color: grey;
  pointer-events: none;
  cursor: default;
  background-color: #d8d8d8;
  width: 75px;
  height: 28px;
  text-align: center;
  padding-top: 6px;
  border: 3px solid grey;
}
</style>
