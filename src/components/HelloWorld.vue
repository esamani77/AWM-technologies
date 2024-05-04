<template>
  <h1>{{ msg }}</h1>
</template>

<script>
const { msg, ...props } = defineProps(["msg"]);
</script>

<style></style>
