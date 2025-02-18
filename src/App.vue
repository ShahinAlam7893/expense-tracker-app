// App.vue
<template>
  <div class="container mt-5">
    <h2 class="text-center">Expense Tracker App</h2>
    <AddTransaction @add-transaction="addTransaction" />
    <TransactionList 
      :transactions="transactions" 
      @delete-transaction="deleteTransaction" 
      @filter-type="filterType"/>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import AddTransaction from './components/AddTransaction.vue';
import TransactionList from './components/TransactionList.vue';

export default {
  components: { AddTransaction, TransactionList },
  setup() {
    const transactions = ref([]);
    const filteredType = ref('all');
    
    onMounted(() => {
      const savedTransactions = localStorage.getItem('transactions');
      if (savedTransactions) transactions.value = JSON.parse(savedTransactions);
    });

    const addTransaction = (transaction) => {
      transactions.value.push(transaction);
      localStorage.setItem('transactions', JSON.stringify(transactions.value));
    };

    const deleteTransaction = (index) => {
      transactions.value.splice(index, 1);
      localStorage.setItem('transactions', JSON.stringify(transactions.value));
    };

    const filterType = (type) => {
      filteredType.value = type;
    };

    return { transactions, addTransaction, deleteTransaction, filterType };
  }
};
</script>

<style>
  @import url(style.css);
</style>