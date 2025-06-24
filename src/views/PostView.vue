<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'
import { RouterLink } from 'vue-router'

const props = defineProps({
  id: {
    type: String,
    required: true,
  },
})

const postInfos = ref([])

onMounted(async () => {
  try {
    const { data } = await axios.get(`https://jsonplaceholder.typicode.com/posts/${props.id}`)
    console.log(data)
    postInfos.value = data
  } catch (error) {
    console.log(error)
  }
})
</script>
<template>
  <main>
    <p v-if="postInfos.length === 0">Chargement en cours</p>
    <div v-else>
      <h1>{{ postInfos.title }}</h1>
      <RouterLink
        :to="{
          name: 'home',
        }"
      >
        Go to homepage
      </RouterLink>
    </div>
  </main>
</template>

<style scoped></style>
