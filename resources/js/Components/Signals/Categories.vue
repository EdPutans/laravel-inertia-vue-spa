<script lang="tsx" setup>
import 'bootstrap/dist/css/bootstrap.css';
import 'bootstrap/dist/js/bootstrap.js';
import { ref } from 'vue';

const categories = ref([{ name: 'Foo' }, { name: 'Bar' }])

defineProps({
  categories: Array,
});

</script>
<template>
  <div>
    <!-- <div v-for="category in $props.categories"> -->
    <div v-for="category in categories" class="bg-primary rounded mb-2">
      {{ category.name }}
    </div>

  </div>
</template>