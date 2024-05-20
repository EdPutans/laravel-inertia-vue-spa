<script lang="tsx" setup>
// import 'bootstrap/dist/css/bootstrap.css';
// import 'bootstrap/dist/js/bootstrap.js';

/**
 *  "identifier": "App\\Signals\\AbstractSignalCategory",
    "name": "Guests",
    "icon": "fas fa-users",
    "description": "Signals related to guests.",
    "signals":
    */
const props = defineProps({
  signal: {
    type: Object,
    required: false,
  },
});

</script>
<template>
  <div>
    <h3 class="h5 ml-4 text-black bold">Signal details</h3>
    <div style="max-height: 500px; overflow: auto;">
      <p class="font-weight-bold">{{ props.signal?.name }}</p>
      <p class="p">
        More details, usage and customisation walkthroughs will be added here.
      </p>
    </div>
  </div>

</template>