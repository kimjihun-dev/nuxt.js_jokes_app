<template>
  <div>
    <h2>{{ joke }}</h2>
    <hr>
    <small>JOKE ID : {{ $route.params.id }}</small><br>
    <nuxt-link to="/jokes">
      LIST
    </nuxt-link>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      joke: {}
    }
  },
  async created () {
    const config = {
      headers: {
        Accept: 'application/json'
      }
    }

    try {
      const res = await axios.get(`https://icanhazdadjoke.com/j/${this.$route.params.id}`, config)
      this.joke = res.data.joke
    } catch (err) {
      // eslint-disable-next-line no-console
      console.log(err)
    }
  },
  head () {
    return {
      title: this.joke,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Best place for corny dad jokes'
        }
      ]
    }
  }
}
</script>

<style>

</style>
