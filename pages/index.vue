<template>
  <p v-if="$fetchState.pending">
    กำลังโหลด...
  </p>
  <div v-else>
    <h1>Nuxt Mountains</h1>
    <ul>
      <li v-for="(mountain, index) of mountains" :key="index">
        <nuxt-link :to="`/${mountain.id}`">
          {{ mountain.title }}
        </nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  async fetch () {
    this.mountains = await fetch(
      'https://api.nuxtjs.dev/posts'
    ).then(res => res.json())
  },
  data () {
    return {
      mountains: []
    }
  }
}
</script>
