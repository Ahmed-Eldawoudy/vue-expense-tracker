<template>
  <h3>History</h3>
  <ul id="list" class="list" v-if="transactions.length !== 0">
    <TransitionGroup name="list" tag="ul">
      <li
        v-for="transaction in transactions"
        :class="transaction.amount > 0 ? 'plus' : 'minus'"
        :key="transaction.id">
        {{ transaction.text }} <span>${{ transaction.amount }}</span>
        <button class="delete-btn" @click="onDeleteTransation(transaction)">
          x
        </button>
      </li>
    </TransitionGroup>
  </ul>
  <div v-else>No History...</div>
</template>

<script setup>
const props = defineProps({
  transactions: { type: Array, required: true },
});
//
const emit = defineEmits(["deleteTransaction"]);
function onDeleteTransation(obj) {
  emit("deleteTransaction", obj);
}
//
</script>

<style scoped>
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>
