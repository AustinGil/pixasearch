<template>
  <div id="app" class="container-fluid">
    <div class="row">
      <div class="col-md-4">search</div>
      <div class="col-md-8">
        <div v-if="isLoading" class="loader">Loading...</div>
        <div v-else class="results row">
          <div v-for="result in results" class="col-sm-6 col-md-4">
            <img :key="result.id" :src="result.previewURL">
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
      apiKey: '6400514-7eedc3bc38ebd6c5736077941', // Use environment variables on real project
      isLoading: true,
      results: []
    }
  },
  methods: {
    fetchImages(params) {
      this.isLoading = true
      // Could also use axios for compatibility
      fetch(`https://pixabay.com/api/?key=${this.apiKey}`)
        .then((response) => response.json())
        .then((response) => {
          console.log(response)
          this.results = response.hits;
          this.isLoading = false
        });
    }
  },
  created() {
    this.fetchImages();
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
