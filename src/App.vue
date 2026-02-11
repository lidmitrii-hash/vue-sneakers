<script setup>
import { ref, provide, watch, computed } from 'vue'


import Header from './components/Header.vue'
import Drawer from './components/Drawer.vue'
import Authorization from './components/Authorization.vue'
/* Корзина */

const cart = ref([])

const drawerOpen = ref(false)

const totalPrice = computed(() => cart.value.reduce((acc, item) => acc + item.price, 0))

const authorizationOpen = ref(false)

const closeAuthorization = () => {
  authorizationOpen.value = false
}
const openAuthorization = () => {
  authorizationOpen.value = true
}

const closeDrawer = () => {
  drawerOpen.value = false
}

const openDrawer = () => {
  drawerOpen.value = true
}

const sortBy = ref('');
const searchQuery = ref('');

const addToCart = (item) => {
  cart.value.push(item)
  item.isAdded = true
}

const removeFromCart = (item) => {
  cart.value.splice(cart.value.indexOf(item), 1)
  item.isAdded = false
}


watch(
  cart, 
  () => {
    localStorage.setItem('cart', JSON.stringify(cart.value))
  },
  { deep: true }
)

provide('cart', {
  cart,
  closeDrawer,  
  openDrawer,
  addToCart,
  removeFromCart,
  openAuthorization,
  closeAuthorization
  })
  
/* Корзина */

</script>



<template>
<Authorization 
v-if="authorizationOpen" 
/>
<Drawer 
v-if="drawerOpen" 
:total-price="totalPrice" 
 

/>
<div class="w-4/5 m-auto bg-white rounded-xl shadow-xl mt-14">
  <Header :total-price="totalPrice" @open-drawer="openDrawer" @open-authorization="openAuthorization" />

  <div class="p-10">
    <router-view></router-view> 
  </div>
</div>
</template>
