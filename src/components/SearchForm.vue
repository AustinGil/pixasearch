<template>
  <div class="search-form-container card card-block">
    <button class="btn btn-primary" type="button" data-toggle="collapse" data-target="#search-form" aria-expanded="false" aria-controls="search-form">
      Toggle Search Form
    </button>
    <form id="search-form" @submit.prevent="submitForm($event)" class="collapse">
      <div class="form-group">
        <label>
          Search
          <input type="text" name="q" class="form-control" maxlength="100">
        </label>
      </div>
      <!-- <div class="form-check">
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

                                      Orientation Category Min_width Min_height Editors_choice safesearch -->

      <!-- <div class="form-group">
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
                                    </div> -->
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script>
export default {
  props: ['formSubmitted'],
  methods: {
    submitForm(event) {
      console.log(event.target)
      let options = {
        per_page: 10
      }
      this.$emit('formSubmitted', options)
    }
  }
}
</script>

<style >

</style>
