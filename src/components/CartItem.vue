<script setup>
const emit = defineEmits(['onClickRemove'])

defineProps({
    id: Number,
    title: String,
    imageUrl: String,
    price: Number,
    
})
</script>

<template>
    
    <div class="flex items-center border border-slate-200 p-4 rounded-xl">
        <img class="w-20 h-20" :src="imageUrl" :alt="title">

        <div class="flex flex-col flex-1">
            <p>{{ title }}</p>

            <div class="flex justify-between mt-2">
                <b class="flex-1">{{ price }} тг.</b>
                <img @click="emit('onClickRemove')" class="opacity-60 hover:opacity-100 cursor-pointer transition" src="/close.svg" alt="">
            </div>
        </div>
    </div>

</template>