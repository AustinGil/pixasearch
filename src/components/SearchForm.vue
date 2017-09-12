<template>
  <div class="search-form-container card card-block">
    <button class="hide-md btn btn-primary" type="button" data-toggle="collapse" data-target="#search-form" aria-expanded="false" aria-controls="search-form">
      Toggle Search Form
    </button>

    <form id="search-form" @submit.prevent="submitForm($event)" class="collapse">
      <div class="form-group">
        <label>
          Search
          <input type="text" name="q" class="form-control" maxlength="100">
        </label>
      </div>

      <div class="form-group">
        <label>Image Type
          <select class="form-control" name="image_type">
            <option>All</option>
            <option>Photo</option>
            <option>Illustration</option>
            <option>Vector</option>
          </select>
        </label>
      </div>

      <div class="form-group">
        <label>Orientation
          <select class="form-control" name="orientation">
            <option>All</option>
            <option>Horizontal</option>
            <option>Vertical</option>
          </select>
        </label>
      </div>

      <div class="form-group">
        Sort Order
        <div class="form-check">
          <label class="form-check-label">
            <input type="radio" class="form-check-input" name="order" value="default" checked> Default
          </label>
        </div>
        <div class="form-check">
          <label class="form-check-label">
            <input type="radio" class="form-check-input" name="order" value="popular"> Popular
          </label>
        </div>
        <div class="form-check">
          <label class="form-check-label">
            <input type="radio" class="form-check-input" name="order" value="latest"> Latest
          </label>
        </div>
      </div>

      <div class="form-group">
        <label>Categories
          <select class="form-control" name="category">
            <option>Fashion</option>
            <option>Nature</option>
            <option>Backgrounds</option>
            <option>Science</option>
            <option>Education</option>
            <option>People</option>
            <option>Feelings</option>
            <option>Religion</option>
            <option>Health</option>
            <option>Places</option>
            <option>Animals</option>
            <option>Industry</option>
            <option>Food</option>
            <option>Computer</option>
            <option>Transportation</option>
            <option>Buildings</option>
            <option>Business</option>
            <option>Music</option>
          </select>
        </label>
      </div>

      <div class="form-group">
        <label>
          Min Width
          <input type="number" name="min_width" class="form-control number" min="0">
        </label>
      </div>

      <div class="form-group">
        <label>
          Min Height
          <input type="number" name="min_height" class="form-control number" min="0">
        </label>
      </div>

      <div class="form-check">
        <label class="form-check-label">
          <input type="checkbox" name="editors_choice" class="form-check-input"> Editor's Choice
        </label>
      </div>

      <div class="form-check">
        <label class="form-check-label">
          <input type="checkbox" name="safesearch" class="form-check-input"> Safesearch
        </label>
      </div>

      <!-- Orientation Category Min_width Min_height Editors_choice safesearch -->
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
@media (min-width: 768px) {
  .hide-md {
    display: none;
  }
  #search-form {
    display: block;
  }
}
</style>
