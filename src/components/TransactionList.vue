<template>
    <div class="mt-4">
      
      <!-- <div class="mb-3">
        <button @click="$emit('filter-type', 'all')">All</button>
        <button @click="$emit('filter-type', 'income')">Income</button>
        <button @click="$emit('filter-type', 'expense')">Expense</button>
      </div> -->

          <div class="form-check form-check-inline">
          <input class="form-check-input" type="radio" name="flexRadioDisabled" id="flexRadioDisabled" checked>
          <label class="form-check-label" for="flexRadioDisabled">
            All
          </label>
        </div>
        <div class="form-check form-check-inline">
          <input class="form-check-input" type="radio" name="flexRadioDisabled" id="flexRadioCheckedDisabled">
          <label class="form-check-label" for="flexRadioCheckedDisabled">
            Income
          </label> 
        </div>
        <div class="form-check form-check-inline">
          <input class="form-check-input" type="radio" name="flexRadioDisabled" id="flexRadioCheckedDisabled">
          <label class="form-check-label" for="flexRadioCheckedDisabled">
            Expense
          </label>
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
  