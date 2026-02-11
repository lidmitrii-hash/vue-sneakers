<script setup>

import axios from 'axios'
import { ref, inject, computed } from 'vue'

import DrawerHead from './DrawerHead.vue'
import CartItemList from './CartItemList.vue'
import InfoBlock from './InfoBlock.vue'


const props = defineProps({
    totalPrice: Number,
})

const {cart, closeDrawer} = inject('cart')

const isCreating = ref(false)
const orderId = ref(null)

const createOrder = async () => {
  try {
    isCreating.value = true

    const { data } = await axios.post('https://d95a793e492c599a.mokky.dev/orders', {
      items: cart.value,
      totalPrice: props.totalPrice.value,
    })

    cart.value = []

    orderId.value = data.id 
  } catch (err) {
    console.log(err)
  } finally {
    isCreating.value = false
  }
}

const cartIsEmpty = computed(() => cart.value.length === 0)

const buttonDisabled = computed(() => isCreating.value || cartIsEmpty.value)
</script>


<template>
<div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-70"></div>
<div class="bg-white w-96 h-full fixed top-0 right-0 z-20 p-8">
    <DrawerHead />


    <div v-if="!totalPrice || orderId" class="flex h-full items-center">
    <InfoBlock 
    v-if="!totalPrice && !orderId"
    title="Корзина пустая" 
    description="Добавьте хотя бы одну пару кроссовок, чтобы сделать заказ." 
    image-url="/package-icon.png" 
    />

    <InfoBlock 
    v-if="orderId"
    title="Заказ Оформлен" 
    :description="`Ваш заказ #${orderId} скоро будет доставлен`" 
    image-url="/order-success-icon.png" 
    />
    </div>


    <div v-else>
    <CartItemList />
    
    <div class="flex flex-col gap-4 my-7">
        <div class="flex gap-2">
            <span>Итого:</span>
            <div class="flex-1"></div>
            <b>{{ totalPrice }} тг</b>
        </div>

        <button 
    :disabled="buttonDisabled"
    @click="createOrder"
    class="transition bg-lime-500 w-full rounded-xl py-3 text-white disabled:bg-slate-300 hover:bg-lime-600 active:bg-lime-700 cursor-pointer"
    >
    Оформить заказ
        </button>


    </div>
    </div>
</div>
</template>