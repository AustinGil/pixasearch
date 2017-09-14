<template>
  <div id="app" class="container-fluid">
    <h1>PixaSearch</h1>
    <div class="row">
      <div class="col-md-4">
        <appSearchForm :filters="filters" @formSubmitted="handleFormSubmitted" @formReset="handleFormReset"></appSearchForm>
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
        image_type: 'all',
        orientation: 'all',
        order: 'default',
        category: 'all',
        min_width: '0',
        min_height: '0',
        editors_choice: false,
        safesearch: false,
        per_page: 200
      }
    }
  },
  methods: {
    fetchImages(options) {

      console.log(options)

      // Reset results and set app to loading
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
    handleFormSubmitted() {
      // Get the options based on active filters and send another request
      this.fetchImages(this.filters)
    },
    handleFormReset() {
      // Reset form filters to default values
      this.filters = {
        q: '',
        image_type: 'all',
        orientation: 'all',
        order: 'default',
        category: 'all',
        min_width: '0',
        min_height: '0',
        editors_choice: false,
        safesearch: false,
        per_page: 200
      }
    }
  },
  created() {
    // Send initial request for 200 images
    this.fetchImages({ per_page: 200 });
  }
}
</script>

<style lang="scss">
// Global styles
label {
  width: 100%;
}

button {
  cursor: pointer;
}

img {
  max-width: 100%;
  height: auto;
}

#app {
  font-family: Helvetica, Arial, sans-serif;
  margin-top: 60px;
}

@media (min-width: 768px) {
  .hide-md {
    display: none;
  }
}
</style>
