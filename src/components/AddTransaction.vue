<template>
    <div class="card p-3 mt-3">
      <h4>Add Transaction</h4>
      <form @submit.prevent="handleSubmit">
        <div class="mb-2">
          <label>Title:</label>
          <input v-model="title" class="form-control" required />
        </div>
        <div class="mb-2">
          <label>Amount:</label>
          <input v-model.number="amount" type="number" class="form-control" required />
        </div>
        <div class="mb-2">
          <label>Type:</label>
          <select v-model="type" class="form-control" required>
            <option value="all">All</option>
            <option value="income">Income</option>
            <option value="expense">Expense</option>
          </select>
        </div>
        <button class="btn btn-primary">Add</button>
      </form>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    emits: ['add-transaction'],
    setup(_, { emit }) {
      const title = ref('');
      const amount = ref(0);
      const type = ref('income');
  
      const handleSubmit = () => {
        if (amount.value <= 0) return alert('Amount must be greater than 0');
        emit('add-transaction', { title: title.value, amount: amount.value, type: type.value });
        title.value = '';
        amount.value = 0;
        type.value = 'income';
      };
      
      return { title, amount, type, handleSubmit };
    }
  };
  </script>