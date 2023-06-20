<template>
  <div>
    <h1>List of Items</h1>
    <ul>
      <li v-for="item in items" :key="item.id">{{ item.name }}</li>
    </ul>

    <form @submit.prevent="addItem">
      <input type="text" v-model="newItemName" placeholder="Item name" />
      <button type="submit">Add Item</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      items: [],
      newItemName: ''
    };
  },
  mounted() {
    this.fetchItems();
  },
  methods: {
    fetchItems() {
      axios.get('https://api.example.com/items')
        .then(response => {
          this.items = response.data;
        })
        .catch(error => {
          console.error(error);
        });
    },
    addItem() {
      const newItem = { name: this.newItemName };

      axios.post('https://api.example.com/items', newItem)
        .then(response => {
          this.items.push(response.data);
          this.newItemName = '';
        })
        .catch(error => {
          console.error(error);
        });
    }
  }
};
</script>

<style>
/* Dodaj dowolne style CSS */
</style>

