<template>
  <div class="mx-auto items-start justify-between space-y-3 p-4">
    <h1 class="text-lg font-extrabold">FormHandler</h1>
    <div>
      <StepHandler
        v-if="step === 1"
        v-model="formData.username"
        title="username"
        type="text"
        :isNextBtnDisabled="false"
        :isPrevBtnDisabled="true"
        @nextPageClicked="nextStep"
      />
      <StepHandler
        v-else-if="step === 2"
        v-model="formData.email"
        title="email"
        type="email"
        :isNextBtnDisabled="false"
        :isPrevBtnDisabled="false"
        @nextPageClicked="nextStep"
        @prevPageClicked="prevStep"
      />
      <Description v-else-if="step === 3" :formData="formData" />
    </div>
  </div>
</template>

<script lang="ts" setup>
import StepHandler from "./StepHandler.vue";
import Description from "./../Description.vue";

import { reactive, ref } from "vue";

const step = ref(1);
const formData = ref({
  username: "",
  email: "",
});

const nextStep = () => {
  step.value++;
  console.log(
    "%c formData",
    "background: #FFF; color: #000;padding: 0.25rem;border-radius: 5px",
    formData
  );
};
const prevStep = () => {
  step.value--;
};
console.log(
  "%c step",
  "background: #FFF; color: #000;padding: 0.25rem;border-radius: 5px",
  step
);
console.log(
  "%c formData",
  "background: #FFF; color: #000;padding: 0.25rem;border-radius: 5px",
  formData
);
</script>

<style></style>
