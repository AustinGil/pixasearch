<template>
  <div class="search-form-container card card-block">
    <button class="hide-md btn btn-primary" type="button" data-toggle="collapse" data-target="#search-form" aria-expanded="false" aria-controls="search-form">
      Toggle Search Form
    </button>

    <form id="search-form" @submit.prevent="submitForm($event)" class="collapse">
      <div class="form-group">
        <label>
          Search
          <input type="text" name="q" ref="q" class="form-control" maxlength="100">
        </label>
      </div>

      <div class="form-group">
        <label>Image Type
          <select class="form-control" name="image_type" ref="image_type">
            <option value="all">All</option>
            <option value="photo">Photo</option>
            <option value="illustration">Illustration</option>
            <option value="vector">Vector</option>
          </select>
        </label>
      </div>

      <div class="form-group">
        <label>Orientation
          <select class="form-control" name="orientation" ref="orientation">
            <option value="all">All</option>
            <option value="horizontal">Horizontal</option>
            <option value="vertical">Vertical</option>
          </select>
        </label>
      </div>

      <div class="form-group">
        Sort Order
        <div class="form-check">
          <label class="form-check-label">
            <input type="radio" class="form-check-input" name="order" ref="order" value="default" checked> Default
          </label>
        </div>
        <div class="form-check">
          <label class="form-check-label">
            <input type="radio" class="form-check-input" name="order" ref="order" value="popular"> Popular
          </label>
        </div>
        <div class="form-check">
          <label class="form-check-label">
            <input type="radio" class="form-check-input" name="order" ref="order" value="latest"> Latest
          </label>
        </div>
      </div>

      <div class="form-group">
        <label>Categories
          <select class="form-control" name="category" ref="category">
            <option value="fashion">Fashion</option>
            <option value="nature">Nature</option>
            <option value="backgrounds">Backgrounds</option>
            <option value="science">Science</option>
            <option value="education">Education</option>
            <option value="people">People</option>
            <option value="feelings">Feelings</option>
            <option value="religion">Religion</option>
            <option value="health">Health</option>
            <option value="places">Places</option>
            <option value="animals">Animals</option>
            <option value="industry">Industry</option>
            <option value="food">Food</option>
            <option value="computer">Computer</option>
            <option value="transportation">Transportation</option>
            <option value="buildings">Buildings</option>
            <option value="business">Business</option>
            <option value="music">Music</option>
          </select>
        </label>
      </div>

      <div class="form-group">
        <label>
          Min Width (px)
          <input type="number" name="min_width" ref="min_width" class="form-control number" min="0">
        </label>
      </div>

      <div class="form-group">
        <label>
          Min Height (px)
          <input type="number" name="min_height" ref="min_height" class="form-control number" min="0">
        </label>
      </div>

      <div class="form-check">
        <label class="form-check-label">
          <input type="checkbox" name="editors_choice" ref="editors_choice" class="form-check-input"> Editor's Choice
        </label>
      </div>

      <div class="form-check">
        <label class="form-check-label">
          <input type="checkbox" name="safesearch" ref="safesearch" class="form-check-input"> Safesearch
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
      let options = {
        q: this.$refs.q.value,
        image_type: this.$refs.image_type.value,
        orientation: this.$refs.orientation.value,
        order: this.$refs.order.value,
        category: this.$refs.category.value,
        min_width: this.$refs.min_width.value,
        min_height: this.$refs.min_height.value,
        editors_choice: this.$refs.editors_choice.value,
        safesearch: this.$refs.safesearch.value
      }
      console.log(options)
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
