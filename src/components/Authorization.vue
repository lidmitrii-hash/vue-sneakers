<script setup>
import { inject } from 'vue';

const { closeAuthorization} = inject('cart')

</script>

<template>
    <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-70"></div>
<div class="bg-white rounded-3xl w-108 items-center h-120 fixed top-25 right-130 z-20 p-8">
  <svg 
        @click="closeAuthorization"
        class="opacity-40 cursor-pointer rotate-180 hover:opacity-100 transition hover:translate-x-1"
        width="20" 
        height="16" 
        viewBox="0 0 16 14" 
        fill="none" 
        xmlns="http://www.w3.org/2000/svg"
        >
        <path 
        d="M1 7H14.7143" 
        stroke="black" 
        stroke-width="2" 
        stroke-linecap="round" 
        stroke-linejoin="round"
        />
        <path 
        d="M8.71436 1L14.7144 7L8.71436 13" 
        stroke="black" 
        stroke-width="2" 
        stroke-linecap="round" 
        stroke-linejoin="round"
        />
  </svg>
  <div class="flex mt-5 items-center gap-29">
  <h2 class="text-2xl font-bold mb-8 mt-3">Авторизация</h2>
  <h3 class="text-l text-blue-500 cursor-pointer font-bold mb-4 underline underline-offset-3 hover:-translate-y-1 hover:text-gray-600"> Регистрация</h3>
  </div>
  <input type="text" placeholder="Логин" class="mt-4 border border-gray-300 rounded-lg p-3 w-full">
  <input type="password" placeholder="Пароль" class="mt-4 border border-gray-300 rounded-lg p-3 w-full">

  <div class="flex items-center gap-3 mt-4">
   <input type="checkbox" class="ml-2 h-5 w-5 cursor-pointer"> 
   <h4>Запомнить пароль</h4>
  </div>
    
  
  <button 
    @click="closeAuthorization"
    class="transition bg-gradient-to-tr from-[#004d7a] via-[#00bfb2] to-[#00f2ff] mt-10 w-full rounded-xl py-3 text-white hover:-translate-y-1 active:bg-lime-700 cursor-pointer"
    >
    Войти
  </button>
   
    <h5 class="underline underline-offset-3 mt-4 cursor-pointer hover:-translate-y-1">Забыли пароль?</h5> 
</div>
</template>