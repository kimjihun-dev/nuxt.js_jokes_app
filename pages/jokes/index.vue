<template>
  <section class="joke-list">
    <SearchJokes @search-text="searchText" />
    <Joke v-for="joke in jokes" :id="joke.id" :key="joke.id" :joke="joke.joke" />
  </section>
</template>

<script>
import axios from 'axios'
import Joke from '../../components/Joke'
import SearchJokes from '../../components/SearchJokes'

export default {
  components: {
    // eslint-disable-next-line vue/no-unused-components
    Joke,
    SearchJokes
  },

  data () {
    return {
      jokes: []
    }
  },
  // eslint-disable-next-line require-await
  async created () {
    // eslint-disable-next-line no-unused-vars
    const config = {
      headers: {
        Accept: 'application/json'
      }
    }

    try {
      const res = await axios.get('https://icanhazdadjoke.com/search', config)
      // eslint-disable-next-line no-console
      this.jokes = res.data.results
    } catch (err) {
      // eslint-disable-next-line no-console
      console.log(err)
    }
  },
  methods: {
    async searchText (text) {
      const config = {
        headers: {
          Accept: 'application/json'
        }
      }
      try {
        const res = await axios.get(`https://icanhazdadjoke.com/search?term=${text}`, config)
        // eslint-disable-next-line no-console
        this.jokes = res.data.results
      } catch (err) {
      // eslint-disable-next-line no-console
        console.log(err)
      }
    }
  },
  head () {
    return {
      title: 'Dad Jokes',
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
