<template>
  <div id="app" class="container-fluid">
    <h1>PixaSearch</h1>
    <div class="row">
      <div class="col-md-4">
        <appSearchForm :formSubmitted="formSubmitted"></appSearchForm>
      </div>
      <div class="col-md-8">
        <appImageGrid :isLoading="isLoading" :results="results" :error="error"></appImageGrid>
      </div>
    </div>
  </div>
</template>

<script>
import SearchFrom from './components/SearchForm'
import ImageGrid from './components/ImageGrid'
export default {
  name: 'app',
  components: {
    appSearchForm: SearchFrom,
    appImageGrid: ImageGrid
  },
  data() {
    return {
      // Use environment variables on real project
      apiKey: process.env.API_KEY || '6400514-7eedc3bc38ebd6c5736077941',
      isLoading: true,
      results: [],
      error: ''
    }
  },
  methods: {
    fetchImages(options = { per_page: 200 }) {

      this.isLoading = true
      // Set up initial query
      let url = `https://pixabay.com/api/?key=${this.apiKey}`

      // Append each parameter to the query if we have them
      if (options) {
        Object.keys(options).forEach((key) => {
          url += `&${key}=${options[key]}`
        })
      }

      // Run the API call
      fetch(url)
        .then((response) => {
          if (!response.ok) {
            throw Error(response.statusText);
          }
          return response.json()
        })
        .then((response) => {
          // console.log(response)
          this.results = response.hits;
          this.isLoading = false
        })
        .catch((err) => {
          console.log(err)
          this.error = err.message
          this.isLoading = false
        });
    }
  },
  created() {
    this.fetchImages();
    this.$on('formSubmitted', (payload) => {
      console.log(payload)
    });
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.results {
  img {
    margin-top: 15px;
    margin-bottom: 15px;
  }
}
</style>
