<script lang="tsx" setup>
import 'bootstrap/dist/css/bootstrap.css';
import 'bootstrap/dist/js/bootstrap.js';
import { ref } from 'vue';
import Categories from './Categories.vue';

defineProps({
  onSubmit: Function,
  onClose: Function,
});

const open = ref(true);

function toggle() {
  console.log('toggle')
  open.value = !open.value
}
</script>


<template>
  <div v-if="open" class="modal fade bd-example-modal-lg show" tabindex="-1" role="dialog" style="display: block;">
    <div class="modal-dialog modal-lg" role="document">
      <div class="modal-content">
        <div class="modal-header d-flex justify-content-between">
          <h5 class="modal-title">Modal title</h5>
          <button type="button" class="close" aria-label="Close" :on-click="toggle">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <div class="container">
            <div class="row">
              <div class="col">
                <Categories />
              </div>
              <div class="col">
                <Selection />
              </div>
              <div class="col">
                <Explainer />
              </div>
            </div>
          </div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-primary" v-on:click="$props.onSubmit">Save changes</button>
          <button type="button" class="btn btn-secondary" v-on:click="toggle">Close</button>
        </div>
      </div>
    </div>
  </div>
</template>
