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
  hoveredOverSignal: {
    type: Object || null,
    required: false,
  },
});

</script>
<template>
  <div v-if="hoveredOverSignal">
    <h3 class="h5 ml-4 text-black bold">Explanation</h3>
    <div style="max-height: 500px; overflow: auto;">
      <p class="p">
        You have selected <b>{{ props.hoveredOverSignal?.name }}</b> More details, usage and customisation will be added
        here.
      </p>
    </div>
  </div>

</template>