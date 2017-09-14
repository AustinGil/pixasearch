<template>
  <div id="app" class="container-fluid">
    <h1>PixaSearch</h1>
    <div class="row">
      <div class="col-md-4">
        <appSearchForm :filters="filters" v-on:formSubmitted="handleFormSubmitted($event)"></appSearchForm>
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
      error: '',
      filters: {
        q: '',
        image_type: '',
        orientation: '',
        order: '',
        category: '',
        min_width: '',
        min_height: '',
        editors_choice: '',
        safesearch: '',
        per_page: 200
      }
    }
  },
  methods: {
    fetchImages(options) {
      this.results = []
      this.isLoading = true
      // Set up initial query
      let url = `https://pixabay.com/api/?key=${this.apiKey}`

      // Append each parameter to the query if we have them
      if (options) {
        Object.keys(options).forEach((key) => {
          url += `&${key}=${options[key]}`
        })
      }

      console.log(url)

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
    },
    handleFormSubmitted(options) {
      // Object.keys(options).forEach((key) => {
      //   url += `&${key}=${options[key]}`
      // })
      options = this.filters
      // Send another API fetch
      this.fetchImages(options)
    }
  },
  created() {
    this.fetchImages({ per_page: 200 });
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
