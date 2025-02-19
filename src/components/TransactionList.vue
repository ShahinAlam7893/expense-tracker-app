<template>
  <div class="mt-4">
    <div class="mb-3">
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="radio" name="filter" id="all" value="all" v-model="selectedFilter">
        <label class="form-check-label" for="all">All</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="radio" name="filter" id="income" value="income" v-model="selectedFilter">
        <label class="form-check-label" for="income">Income</label> 
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="radio" name="filter" id="expense" value="expense" v-model="selectedFilter">
        <label class="form-check-label" for="expense">Expense</label>
      </div>
    </div>

    <table class="table table-bordered">
      <thead>
        <tr>
          <th>Title</th>
          <th>Amount</th>
          <th>Type</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(transaction, index) in filteredTransactions" :key="index">
          <td>{{ transaction.title }}</td>
          <td :class="{ 'fw-bold': transaction.amount >= 500, 'text-success': transaction.type.toLowerCase() === 'income', 'text-danger': transaction.type.toLowerCase() === 'expense' }">
            ${{ transaction.amount }}
          </td>
          <td>{{ transaction.type.toUpperCase() }}</td>
          <td><button @click="$emit('delete-transaction', index)" class="btn btn-danger">Delete</button></td>
        </tr>
        <tr v-if="filteredTransactions.length === 0">
          <td colspan="4" class="text-center">No transactions recorded yet.</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import { ref, computed } from 'vue';

export default {
props: ['transactions'],
setup(props) {
  const selectedFilter = ref('all');

  const filteredTransactions = computed(() => {
    console.log("Selected Filter:", selectedFilter.value);
    console.log("Transactions:", props.transactions);

    if (selectedFilter.value === 'all') return props.transactions;
    return props.transactions.filter(transaction => transaction.type.toLowerCase() === selectedFilter.value);
  });

  return { selectedFilter, filteredTransactions };
}
};
</script>
