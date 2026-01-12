<script setup>
import { computed, onMounted, ref } from 'vue';
import { useToast } from 'vue-toastification';


const items = ref([])

const form = ref({
  text: '',
  price: 0
})

const toast = useToast();

onMounted(() => {
  const savedItems = localStorage.getItem('items')

  if (savedItems) {
    items.value = JSON.parse(savedItems)
  }
})

const addItem = () => {

  if (!form.value.text || form.value.price === ''){
    toast.error('Both fields must be filled.');
    return;
  }

  items.value.push({
    text: form.value.text,
    price: Number(form.value.price)
 })

 localStorage.setItem('items', JSON.stringify(items.value))

 toast.success("Transaction added!", {
   position: 'top-center'
 });

  form.value.text = ''
  form.value.price = ''
}


const income = computed(() => {
  return items.value
  .filter(item => item.price > 0)
  .reduce((sum, item) => sum + item.price, 0)
})


const expense = computed(() => {
  return items.value
    .filter(item => item.price < 0)
    .reduce((sum, item) => sum + item.price, 0)
})


const balance = computed(() => {
    return income.value + expense.value
})


const deleteItem = (itemToDelete) => {
  items.value = items.value.filter(item => item !== itemToDelete)
  localStorage.setItem('items', JSON.stringify(items.value))
  toast.info('Transaction removed')
}

</script>

<template>
  <h2>Expense Tracker</h2>
  <h4>Your Balance</h4>
  <h1 id="balance">${{ balance }}</h1>


  <div class="inc-exp-container">
    <div>
      <h4>Income</h4>
      <p id="money-plus" class="money plus">+${{ income }}</p>
    </div>
    <div>
      <h4>Expense</h4>
      <p id="money-minus" class="money minus">-${{ expense }}</p>
    </div>
  </div>

  <h3>History</h3>
  <ul id="list" class="list">
    <li v-for="item in items" :key="item.text" :class="item.price >= 0 ? 'plus' : 'minus'">
      {{ item.text }}<span>${{ item.price }}</span>
      <button @click="deleteItem(item)" class="delete-btn">
        x
      </button>
    </li>
  </ul>


   <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="addItem">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" placeholder="Enter text..." v-model="form.text"/>
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input
        type="number"
        id="amount"
        placeholder="Enter amount..."
        v-model="form.price"
      />
    </div>
    <button class="btn">Add transaction</button>
  </form>

</template>