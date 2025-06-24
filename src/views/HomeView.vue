<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'
import { RouterLink } from 'vue-router'

const postLists = ref([])

onMounted(async () => {
  try {
    const { data } = await axios.get('https://jsonplaceholder.typicode.com/posts') // destructur axios = data
    // console.log(data)
    postLists.value = data
  } catch (error) {
    console.log(error)
  }
})
</script>

<template>
  <main>
    <p v-if="postLists.length === 0">Chargement en cours ...</p>
    <div v-else>
      <h1>Hello World !</h1>
      <RouterLink
        v-for="post in postLists"
        :key="post.id"
        :to="{ name: 'post', params: { id: post.id } }"
      >
        <article>
          <h2>{{ post.title }}</h2>
        </article>
      </RouterLink>
    </div>
  </main>
</template>

<style scoped>
main {
  padding: 30px;
  background-color: antiquewhite;
}
article {
  border: 1px solid green;
  padding: 24px;
  margin: 0 0 8px 0;
  color: green;
}
a {
  color: inherit;
  text-decoration: none;
}
</style>
