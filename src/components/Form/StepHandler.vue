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
    <small v-if="validateUsername()">Invalid Username.</small>
    <small v-if="validateEmail()">Invalid email address.</small>
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
        :disabled="isNextBtnDisabled || validateEmail() || validateUsername()"
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
  model = text;
}

const nextPageClick = () => {
  emit("nextPageClicked");
};
const pervPageClick = () => {
  emit("prevPageClicked");
};

const validateUsername = () => {
  if (title === "email") return false;
  if (model.value === "" || (model.value as any).includes(" ")) {
    return true;
  }
  return false;
};
const validateEmail = () => {
  if (title === "username") return false;
  if (
    !(model.value as any).includes("@") ||
    !(model.value as any).includes(".")
  ) {
    return true;
  }
  return false;
};
</script>

<style></style>
