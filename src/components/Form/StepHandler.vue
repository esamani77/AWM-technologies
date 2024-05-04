<template>
  <div>
    <h4 class="">{{ title }}</h4>
    <input
      :type="type"
      :name="title"
      :id="title"
      v-model="model"
      @change="update"
      class="border p-3 my-2"
    />
    <small v-if="type === 'username' && !validateUsername()"
      >Invalid Username.</small
    >
    <small v-if="type === 'email' && !validateEmail()"
      >Invalid email address.</small
    >
    <div class="flex space-x-1 justify-between">
      <button
        type="button"
        class="prev-btn border py-2 px-6 border-blue-700 rounded w-1/2 disabled:text-gray-200"
        :disabled="isPrevBtnDisabled"
        @click="pervPageClick"
        id="btn-prev"
      >
        prev
      </button>
      <button
        type="button"
        class="next-btn py-2 px-6 bg-blue-700 rounded w-1/2 text-white disabled:bg-gray-400"
        :disabled="isNextBtnDisabled || model === ''"
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
const props = defineProps([
  "title",
  "type",
  "text",
  "isPrevBtnDisabled",
  "isNextBtnDisabled",
]);
const { title, type, text, isPrevBtnDisabled, isNextBtnDisabled } = props;

function update() {
  console.log("🚀 ~ model:", model);
  //   model.value++;
  model = text;
}

const nextPageClick = () => {
  emit("nextPageClicked");
};
const pervPageClick = () => {
  emit("prevPageClicked");
};

const validateUsername = () => {
  // You can implement username validation logic here
  if (model) {
    return true;
  }
  return false;
};
const validateEmail = () => {
  // You can implement email validation logic here
  // if (!model.includes("@") || !model.includes(".")) {
  //   return true;
  // }
  return false;
};
console.log("🚀 ~ model:", model, text);
</script>

<style></style>
