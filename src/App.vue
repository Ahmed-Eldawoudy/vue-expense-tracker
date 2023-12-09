<template>
  <Header />
  <div class="container">
    <Balance :income="income" :expense="expense" />
    <IncomeExpenses :income="income" :expense="expense" />
    <TransactionList
      :transactions="transactions"
      @deleteTransaction="handelTransactionDele" />
    <AddTransaction @addTransactions="handleTransactionSubmitted" />
  </div>
</template>

<script setup>
//
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";
//
import { ref, computed } from "vue";
import { v4 as uuidv4 } from "uuid";
//
const transactions = ref([
  { id: uuidv4(), text: "Ryan", amount: -19.99 },
  { id: uuidv4(), text: "Virginia", amount: 69 },
  { id: uuidv4(), text: "Don", amount: -83 },
  { id: uuidv4(), text: "Lloyd", amount: 69 },
]);
//
const income = computed(() => {
  return transactions.value
    .filter((t) => t.amount > 0)
    .reduce(function (acc, obj) {
      return acc + obj.amount;
    }, 0);
});
//
const expense = computed(() => {
  return transactions.value
    .filter((t) => t.amount < 0)
    .reduce(function (acc, obj) {
      return acc + obj.amount;
    }, 0);
});
//
const handelTransactionDele = (obj) => {
  transactions.value = transactions.value.filter((t) => t.id !== obj.id);
};
//
function handleTransactionSubmitted(transactionData) {
  transactions.value.push({
    id: uuidv4(),
    text: transactionData.text,
    amount: transactionData.amount,
  });
}
//
</script>

<style scoped></style>
