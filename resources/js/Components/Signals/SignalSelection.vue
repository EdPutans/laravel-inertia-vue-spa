<script lang="tsx" setup>
import 'bootstrap/dist/css/bootstrap.css';
import 'bootstrap/dist/js/bootstrap.js';
import { computed } from 'vue';


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
  setHoveredOverSignal: {
    type: Function,
    required: true,
  },
  hoveredOverSignal: {
    type: Object,
    required: false,
  },
  setSelectedSignal: {
    type: Function,
    required: true,
  },
  selectedSignal: {
    type: Object,
    required: false,
  },
});

const getButtonHighlight = (signal) => {
  return props.hoveredOverSignal?.name === signal.name ? 'btn-primary' : 'btn-transparent'
}



const signals = computed(() => props.selectedCategory.signals);

</script>
<template>
  <div class="rounded w-full border-right h-40">
    <h3 class="h5 ml-4 text-black bold">Signals</h3>
    <div style="max-height: 500px; overflow: auto;">
      <div class="btn-group-vertical" style="display: block;" role="group">
        <button v-bind:key="signal.name" v-for="signal in signals" type="button" class="btn text-start rounded"
          :class="getButtonHighlight(signal)" v-on:mouseenter="() => $props.setHoveredOverSignal(signal)"
          v-on:mouseleave="() => $props.setHoveredOverSignal(null)" v-on:click="() => $props.setSelectedSignal(signal)">
          {{ signal.name }}
        </button>
      </div>
    </div>
  </div>
</template>