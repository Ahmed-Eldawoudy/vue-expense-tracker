<template>
  <h4>Your Balance</h4>
  <h1 id="balance">${{ (expense + income).toFixed(2) }}</h1>
</template>

<script setup>
const props = defineProps({
  income: { type: Number, required: true },
  expense: { type: Number, required: true },
});
</script>
