<script setup>
import axios from 'axios'
import { onMounted, ref } from 'vue'


import CardList from '../components/CardList.vue'

const favorites = ref([])

const addToFavorite = async (item) => {
  try {
  if (!item.isFavorite) {
    const obj = {
    productId: item.id,
    item
  }

  item.isFavorite = true

  const { data } = await axios.post('https://d95a793e492c599a.mokky.dev/favorites', obj)

  
  item.favoriteId = data.id
  
  console.log(data)
  } else {
    item.isFavorite = false
    await axios.delete(`https://d95a793e492c599a.mokky.dev/favorites/${item.favoriteId}`)
    item.favoriteId = null
  }
    } catch (err) {
    console.log(err)
  }
}




onMounted(async () => {
    try {
    const {data} = await axios.get(
        'https://d95a793e492c599a.mokky.dev/favorites?_relations=items'
    )

    favorites.value = data.map((obj) => obj.item)

    } catch(err) {
        console.log(err)
    }
})

</script>


<template>
<h2 class="text-3xl font-bold mb-8">Избранное</h2>

<CardList 

:items="favorites" 
is-favorites=""
@addToFavorite="addToFavorite"

/> 

</template>