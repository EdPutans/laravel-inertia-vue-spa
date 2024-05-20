<script lang="tsx" setup>
import 'bootstrap/dist/css/bootstrap.css';
import 'bootstrap/dist/js/bootstrap.js';


/**
 *  "identifier": "App\\Signals\\AbstractSignalCategory",
    "name": "Guests",
    "icon": "fas fa-users",
    "description": "Signals related to guests.",
    "signals":
    */
const props = defineProps({
  selectedCategory: {
    type: Object,
    required: true,
  },
  categories: {
    type: Object,
    required: true,
  },
  setSelectedCategory: {
    type: Function,
    required: true,
  },
});

const categoriesAsArray = Object.values(props.categories)

const getButtonHighlight = (category) => {
  return props.selectedCategory.name === category.name ? 'btn-primary' : 'btn-transparent'
}

</script>
<!-- @TODO:  convert this into a listicle component and reuse across the modal func-->
<template>
  <div class="rounded w-full border-right h-40">
    <h3 class="h5 ml-4 text-black bold">Categories</h3>
    <div style="max-height: 500px; overflow: auto;">
      <div class="btn-group-vertical" style="display: block;" role="group">
        <button v-bind:key="category.name" v-for="category in categoriesAsArray" type="button"
          class="btn text-start rounded" :class="getButtonHighlight(category)"
          v-on:click="() => $props.setSelectedCategory(category)">
          {{ category.name }}
        </button>
      </div>
    </div>
  </div>
</template>