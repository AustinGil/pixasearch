<template>
  <div class="card card-block">
    <div v-if="isLoading" class="loader">Loading...</div>
    <div v-else-if="error" class="alert alert-danger" role="alert">
      {{ error }}
    </div>
    <div v-else class="results row">
      <div v-for="result in results" :key="result.id" class="col-sm-6 col-md-4">
        <img :src="result.previewURL">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['isLoading', 'results', 'error']
}
</script>

<style lang="scss">
.results {
  img {
    margin-top: 15px;
    margin-bottom: 15px;
  }
}
</style>
