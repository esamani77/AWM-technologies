<template>
  <div>
    <h4 class="">{{ title }}:</h4>
    <input
      :type="type"
      :name="title"
      :id="title.toLowerCase()"
      v-model="model"
      class="border p-3 my-2"
    />
    <br />

    <small v-if="validateUsername()">Invalid Username.</small>
    <small v-if="validateEmail()">Email: Invalid email address.</small>
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
        :disabled="isNextBtnDisabled"
        @click="nextPageClick()"
        id="btn-next"
      >
        next
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

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
// const showError = ref(false);
// function update() {
//   model = text;
// }

const nextPageClick = () => {
  if (
    (title === "Username" && validateUsername()) ||
    (title === "Email" && validateEmail())
  ) {
    // showError.value = true;
  } else {
    // showError.value = false;

    emit("nextPageClicked");
  }
};
const pervPageClick = () => {
  emit("prevPageClicked");
};

const validateUsername = () => {
  if (title === "Email") return false;

  const isValidLenght =
    (model.value as any).length > 3 && (model.value as any).length < 20;

  if (
    model.value === "" ||
    (model.value as any).includes(" ") ||
    !isValidLenght
  ) {
    return true;
  }
  return false;
};
const validateEmail = () => {
  if (title === "Username") return false;
  if (
    !(model.value as any).includes("@") ||
    (model.value as any).includes(" ") ||
    !(model.value as any).includes(".")
  ) {
    return true;
  }
  return false;
};
</script>

<style></style>
