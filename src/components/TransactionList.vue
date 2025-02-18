<template>
    <div class="mt-4">
      <h4>Transaction List</h4>
      <div class="mb-3">
        <button @click="$emit('filter-type', 'all')" class="btn btn-secondary me-2">All</button>
        <button @click="$emit('filter-type', 'income')" class="btn btn-success me-2">Income</button>
        <button @click="$emit('filter-type', 'expense')" class="btn btn-danger">Expense</button>
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
          <tr v-for="(transaction, index) in transactions" :key="index">
            <td>{{ transaction.title }}</td>
            <td :class="{ 'fw-bold': transaction.amount >= 500, 'text-success': transaction.type === 'income', 'text-danger': transaction.type === 'expense' }">
              ${{ transaction.amount }}
            </td>
            <td>{{ transaction.type.toUpperCase() }}</td>
            <td><button @click="$emit('delete-transaction', index)" class="btn btn-danger">Delete</button></td>
          </tr>
          <tr v-if="transactions.length === 0">
            <td colspan="4" class="text-center">No transactions recorded yet.</td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    props: ['transactions']
  };
  </script>
  