<template>
  <div id="app" class="container-fluid">
    <h1>PixaSearch</h1>
    <div class="row">
      <div class="col-md-4">
        <div class="search-form-container card card-block">
          <button class="btn btn-primary" type="button" data-toggle="collapse" data-target="#search-form" aria-expanded="false" aria-controls="search-form">
            Toggle Search Form
          </button>
          <form id="search-form" @submit.prevent="submitForm" class="collapse">
            <div class="form-group">
              <label>
                Search
                <input type="text" name="q" class="form-control" maxlength="100">
              </label>
            </div>
            <div class="form-check">
              Filters
              <label class="form-check-label">
                <input type="checkbox" class="form-check-input"> Image Type
              </label>
              <label class="form-check-label">
                <input type="checkbox" class="form-check-input"> Orientation
              </label>
              <label class="form-check-label">
                <input type="checkbox" class="form-check-input"> Image Type
              </label>
              <label class="form-check-label">
                <input type="checkbox" class="form-check-input"> Image Type
              </label>
              <label class="form-check-label">
                <input type="checkbox" class="form-check-input"> Image Type
              </label>
              <label class="form-check-label">
                <input type="checkbox" class="form-check-input"> Image Type
              </label>
              <label class="form-check-label">
                <input type="checkbox" class="form-check-input"> Image Type
              </label>
            </div>

            Orientation Category Min_width Min_height Editors_choice safesearch

            <div class="form-group">
              Sort Order
              <div class="form-check">
                <label class="form-check-label">
                  <input type="radio" class="form-check-input" name="sort-order" value="default" checked> Default
                </label>
              </div>
              <div class="form-check">
                <label class="form-check-label">
                  <input type="radio" class="form-check-input" name="sort-order" value="popular"> Popular
                </label>
              </div>
              <div class="form-check">
                <label class="form-check-label">
                  <input type="radio" class="form-check-input" name="sort-order" value="latest"> Latest
                </label>
              </div>
            </div>
            <button type="submit" class="btn btn-primary">Submit</button>
          </form>
        </div>
      </div>
      <div class="col-md-8">
        <div class="card card-block">
          <div v-if="isLoading" class="loader">Loading...</div>
          <div v-else-if="error" class="alert alert-danger" role="alert">
            {{ error }}
          </div>
          <div v-else class="results row">
            <div v-for="result in results" class="col-sm-6 col-md-4">
              <img :key="result.id" :src="result.previewURL">
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
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
    },
    submitForm() {
      this.$emit('formSubmitted', 'test')
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
