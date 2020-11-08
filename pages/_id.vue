<template>
  <div>
    <p v-if="$fetchState.pending">
      กำลังโหลด...
    </p>
    <div v-else>
      <h1>{{ id }}: {{ mountain.title }}</h1>
      <img :src="mountain.image" width="400" loading="lazy">
      <br>
      <nuxt-link to="/" class="button--grey">
        กลับ
      </nuxt-link>
      <pre class="text-white">{{ mountain }}</pre>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NameComponent',
  async fetch () {
    this.mountain = await fetch(
      `https://api.nuxtjs.dev/posts/${this.id}`
    ).then(res => res.json())
  },
  data () {
    return {
      mountain: {}
    }
  },
  computed: {
    id () {
      return this.$route.params.id
    }
  },
  head () {
    return {
      title: this.mountain.title
    }
  }
}
</script>
