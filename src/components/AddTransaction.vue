<template>
    <div class="card p-3 mt-3">
      <form @submit.prevent="handleSubmit" class="inputForm">
        <div class="mb-2">
      
          <input v-model="title" class="form-control" placeholder="Title" required />

        </div>
        <div class="mb-2">
        
          <input v-model.number="amount" type="number" class="form-control" required />
        </div>
        <div class="mb-2">
          
          <select v-model="type" class="form-control" aria-placeholder="Type" required>
            
            <option value="income">Income</option>
            <option value="expense">Expense</option>
          </select>
        </div>
        <div>
            <button type="submit" class="btn btn-primary">ADD</button>
          </div>
        
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