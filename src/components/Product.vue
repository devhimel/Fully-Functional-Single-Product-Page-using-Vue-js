<script setup>
import nikeBlack from '../assets/images/nike-black.jpg'
import nikeRed from '../assets/images/nike-red.jpg'
import nikeWhite from '../assets/images/nike-white.jpg'
import {computed, reactive, ref} from "vue";
const navMenu = {
  logo: 'Nike',
  navLinks:{
    link1: 'Home',
    link2: 'About',
    link3: 'Product',
    link4: 'Contact'
  }
}

const productDettails =reactive({
  brandName: 'Nike',
  productName: 'Air Force',
  selectedVariant: 0,
  cart: 0,
  features: [
    'Durable Leather',
    'Secure lace up',
    'Padded ankle collar'
  ],
  variants: [
    {
      variantId: 1,
      variantColor: 'Red',
      variantImage: nikeRed,
      variantQty: 20,
    },
    {
      variantId: 2,
      variantColor: 'White',
      variantImage: nikeWhite,
      variantQty: 5,
    },{
      variantId: 3,
      variantColor: 'Black',
      variantImage: nikeBlack,
      variantQty: 0,
    },
  ]

})
function addToCart() {
  productDettails.cart +=1;
}
function updateImage(index) {
  productDettails.selectedVariant = index;
  console.log(index)
}
const title = computed(()=>{
  return `${productDettails.brandName} ${productDettails.productName}`
})
const productImage = computed(()=>{
  return productDettails.variants[productDettails.selectedVariant].variantImage;
})
const inventory = computed(()=>{
  return productDettails.variants[productDettails.selectedVariant].variantQty;
})
</script>

<template>
  <section>
    <header class="bg-gray-100 shadow-md px-44 py-4">
      <nav class="flex items-center justify-between">
      <a href="" class="font-bold text-2xl text-black">
        Nike
      </a>
        <ul class="flex gap-7">
          <li v-for="(link, index) in navMenu.navLinks" :key="index">
            <a href="#" class="text-lg font-semibold text-gray-700 hover:text-gray-900 transition">{{ link }}</a>
          </li>
        </ul>
        <div>
          <i class="fa-solid fa-basket-shopping text-lg font-semibold text-gray-700 hover:text-gray-900 transition"></i>
          {{ productDettails.cart }}
        </div>
      </nav>
    </header>
    <main class="container mx-auto mt-10">
      <section class="flex gap-10">
        <div >
          <img class="rounded-lg" :src="productImage" alt="">
        </div>
        <div>
          <h1 class="text-4xl font-bold mt-4">
            {{ title }}
          </h1>
          <div class="mt-2">
            <span class="bg-green-600 px-4 py-1 rounded-2xl text-white text-center " v-if="inventory > 10">In Stock</span>
            <span class="bg-orange-400 px-4 py-1 rounded-2xl text-white text-center " v-else-if="inventory <=10 && inventory > 0">Limited Stock</span>
            <span class="bg-red-500 px-4 py-1 rounded-2xl text-white text-center " v-else>Out of Stock</span>
          </div>
          <h4 class="text-xl mt-4 font-semibold">Product Features: </h4>
          <ul class="list-disc ps-5 py-2">
            <li v-for="(feature, index) in productDettails.features" :key="index">{{ feature }}</li>
          </ul>
          <div class="mt-4">
            <span v-for="(variant, index) in productDettails.variants" :key="variant.variantId" class="shadow-md px-8 py-3 border border-gray-300 rounded-md m-1" @mouseover="updateImage(index)" :style="{backgroundColor: variant.variantColor}">
            </span>
          </div>
          <div class="mt-10">
            <button class="px-5 py-3 bg-black text-white rounded-lg" @click="addToCart()" :disabled="inventory <= 0" :class="inventory <= 0 ? 'bg-gray-400' : ''">Add to Cart</button>
          </div>
        </div>
      </section>
    </main>

  </section>
</template>

<style scoped>

</style>