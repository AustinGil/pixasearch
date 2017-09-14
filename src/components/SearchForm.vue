<template>
  <div class="search-form-container card card-block">
    <button class="toggle-search-form hide-md btn btn-primary" type="button" data-toggle="collapse" data-target="#search-form" aria-expanded="false" aria-controls="search-form">
      Toggle Search Form
    </button>

    <form id="search-form" @submit.prevent="submitForm($event)" class="collapse">
      <div class="form-group">
        <label>
          Search
          <input type="text" name="q" ref="q" v-model="filters.q" class="form-control" maxlength="100">
        </label>
      </div>

      <div class="form-group">
        <label>Image Type
          <select class="form-control" name="image_type" v-model="filters.image_type">
            <option value="all">All</option>
            <option value="photo">Photo</option>
            <option value="illustration">Illustration</option>
            <option value="vector">Vector</option>
          </select>
        </label>
      </div>

      <div class="form-group">
        <label>Orientation
          <select class="form-control" name="orientation" v-model="filters.orientation">
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
            <input type="radio" class="form-check-input" name="order" v-model="filters.order" value="default" checked> Default
          </label>
        </div>
        <div class="form-check">
          <label class="form-check-label">
            <input type="radio" class="form-check-input" name="order" v-model="filters.order" value="popular"> Popular
          </label>
        </div>
        <div class="form-check">
          <label class="form-check-label">
            <input type="radio" class="form-check-input" name="order" v-model="filters.order" value="latest"> Latest
          </label>
        </div>
      </div>

      <div class="form-group">
        <label>Categories
          <select class="form-control" name="category" v-model="filters.category">
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
          <input type="number" name="min_width" v-model="filters.min_width" class="form-control number" min="0">
        </label>
      </div>

      <div class="form-group">
        <label>
          Min Height (px)
          <input type="number" name="min_height" v-model="filters.min_height" class="form-control number" min="0">
        </label>
      </div>

      <div class="form-check">
        <label class="form-check-label">
          <input type="checkbox" name="editors_choice" v-model="filters.editors_choice" class="form-check-input"> Editor's Choice
        </label>
      </div>

      <div class="form-check">
        <label class="form-check-label">
          <input type="checkbox" name="safesearch" v-model="filters.safesearch" class="form-check-input"> Safesearch
        </label>
      </div>

      <!-- Orientation Category Min_width Min_height Editors_choice safesearch -->
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script>
export default {
  props: ['filters', 'formSubmitted'],
  methods: {
    submitForm(event) {
      this.$emit('formSubmitted')
    }
  }
}
</script>

<style >
.toggle-search-form {
  margin-bottom: 15px;
}

@media (min-width: 768px) {
  #search-form {
    display: block;
  }
}
</style>
