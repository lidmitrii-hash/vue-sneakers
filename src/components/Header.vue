<script setup> 
defineProps({
  totalPrice: Number,
})

const emit = defineEmits(['openDrawer', 'openAuthorization'])

</script>

<template>

<header class="flex justify-between border-b border-gray-300 px-8 py-8">
  
<router-link to="/">
  <div class="flex items-center gap-4">
      <img src="/logo.png" alt="Logo" class="w-10">
    <div>
      <h2 class="text-xl font-bold uppercase">Sneakers-Shop</h2>
      <p class="text-gray-500">Лучший магазин кроссовок</p>
    </div>
  </div>
</router-link>

<ul class="flex items-center gap-10">
  <li @click="() => emit('openDrawer')" class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black">
    <img src="/cart.svg" alt="">
    <b>{{ totalPrice }} тг.</b>
  </li>

  <router-link to="/favorites"> 
    <li class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black">
    <img src="/heart.svg" alt="">
    <span>Избранное</span>
  </li>
  </router-link>
  
  <li @click="() => emit('openAuthorization')" class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black">
    <img src="/profile.svg" alt="">
    <span>Вход</span>
  </li>
</ul>
</header>

</template>