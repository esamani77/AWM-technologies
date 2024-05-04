<template>
  <div class="mx-auto items-start justify-between space-y-3 p-4">
    <h1 class="text-lg font-extrabold">FormHandler</h1>
    <div>
      <StepHandler
        v-if="step === 1"
        v-model="formData.username"
        :text="formData.username"
        title="Username"
        :type="'text'"
        :isNextBtnDisabled="false"
        :isPrevBtnDisabled="true"
        @nextPageClicked="nextStep"
      />
      <StepHandler
        v-else-if="step === 2"
        v-model="formData.email"
        :text="formData.email"
        title="Email"
        :type="'email'"
        :isNextBtnDisabled="false"
        :isPrevBtnDisabled="false"
        @nextPageClicked="nextStep"
        @prevPageClicked="prevStep"
      />
      <Result
        v-else-if="step === 3"
        :formData="formData"
        @prevPageClicked="prevStep"
      />
    </div>
  </div>
</template>

<script lang="ts" setup>
import StepHandler from "./Form/StepHandler.vue";
import Result from "./Form/Result.vue";

import { reactive, ref } from "vue";

const step = ref(1);
const formData = ref({
  username: "",
  email: "",
});

const nextStep = () => {
  step.value++;
};
const prevStep = () => {
  step.value--;
};
</script>

<style></style>
