<script setup>
const props = defineProps({
  selectedSignal: {
    type: Object,
    required: false,
  },
});

</script>

<template>
  <div class="rounded btn-group-vertical w-full border-right h-40">
    <h3 class="h5 ml-4 text-black bold">Customisation</h3>
    <div style="max-height: 500px; overflow: auto;">
      <p class="p">
      <pre style="max-width: 300px;">{{ JSON.stringify(props.selectedSignal, null, 2) }}</pre>
      </p>
    </div>
  </div>
</template>