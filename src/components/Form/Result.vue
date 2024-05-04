<template>
  <div>
    {{ formData }}
    <div class="flex space-x-1 justify-between">
      <button
        type="button"
        class="prev-btn border py-2 px-6 border-blue-700 rounded w-1/2 disabled:text-gray-200"
        @click="pervPageClick"
        id="btn-prev"
      >
        prev
      </button>
      <button
        type="button"
        class="next-btn py-2 px-6 bg-blue-700 rounded w-1/2 text-white disabled:bg-gray-400"
        :disabled="true"
        @click="nextPageClick()"
        id="btn-next"
      >
        next
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
let model = defineModel();
const emit = defineEmits(["nextPageClicked", "prevPageClicked"]);
const props = defineProps(["formData"]);
const { formData } = props;

const nextPageClick = () => {
  emit("nextPageClicked");
};
const pervPageClick = () => {
  emit("prevPageClicked");
};
</script>
