<template>
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
</template>

<script>
export default {
  props: ['isLoading', 'results', 'error']
}
</script>

<style >

</style>
