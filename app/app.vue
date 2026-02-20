<!-- <template>
  <div>
    <Input v-model="name" label="name" error-message="Error" error />
  </div>
</template>
<script setup lang="ts">
const name = ref("asdasd");

watch(name, (newVal, oldVal) => {
  console.log(newVal, oldVal);
});
</script> -->



<template>
  <div class="p-10">
    <Input
      v-model="name"
      label="Name"
      placeholder="Enter your name"
      clearable
      error
      error-message="Name is required"
    />
  </div>
</template>

<script setup lang="ts">
const name = ref("Hello");

watch(name, (newVal, oldVal) => {
  console.log("New:", newVal);
  console.log("Old:", oldVal);
});
</script>