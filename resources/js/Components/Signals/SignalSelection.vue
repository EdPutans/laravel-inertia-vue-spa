<script lang="tsx" setup>
// import 'bootstrap/dist/css/bootstrap.css';
// import 'bootstrap/dist/js/bootstrap.js';
import { computed } from 'vue';

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

const getButtonHighlightClassName = (signal) => {
  if (props.selectedSignal?.identifier === signal.identifier) return 'btn-primary';
  if (props.hoveredOverSignal?.identifier === signal.identifier) return 'btn-transparent text-primary';

  return 'btn-transparent'
}

const signals = computed(() => props.selectedCategory.signals);

</script>
<template>
  <div class="rounded w-full border-right h-40">
    <button v-if="selectedSignal" v-on:click="() => setSelectedSignal(undefined)"
      class="btn btn-transparent p-0 modal-title">
      <h3 class="h5 ml-4 text-black bold">← &nbsp; Signals</h3>
    </button>
    <h3 v-else class="h5 ml-4 text-black bold">Signals</h3>
    <!-- <h3 class="h5 ml-4 text-black bold">Signals</h3> -->
    <div style="max-height: 500px; overflow: auto;">
      <div class="btn-group-vertical" style="display: block;" role="group">
        <button v-bind:key="signal.name" v-for="signal in signals" type="button" class="btn text-start rounded"
          :class="getButtonHighlightClassName(signal)" v-on:mouseenter="() => $props.setHoveredOverSignal(signal)"
          v-on:mouseleave="() => $props.setHoveredOverSignal(null)" v-on:click="() => $props.setSelectedSignal(signal)">
          {{ signal.name }}
        </button>
      </div>
    </div>
  </div>
</template>