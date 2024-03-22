<template>
  <br>
  <div class="input">
    <input type="text" v-model="ItemInput" placeholder="Enter Item"> <br>
    <input type="number" v-model="ItemInputQuantity" placeholder="Quantity"> <br>
    <button class="add-button" @click="addItem">Add</button>
  </div>
  <br>
</template>

<script>
export default {
  data() {
    return {
      ItemInput: '',
      ItemInputQuantity: 1
    };
  },
  props: {
    items: {
      type: Array,
      required: true
    }
  },
  methods: {
    addItem() {
      if (this.ItemInput.trim() === '') {
        alert('Enter Item First');
        return;
      }

      const foundItem = this.items.find(item => item.name.toLowerCase() === this.ItemInput.toLowerCase());
      if (!foundItem) {
        alert('Item not found');
        return;
      }

      this.$emit('add-item', {
        name: foundItem.name,
        cost: foundItem.cost,
        quantity: this.ItemInputQuantity,
        editable: false,
        newQuantity: 1
      });

      this.ItemInput = '';
      this.ItemInputQuantity = 1;
    }
  }
};
</script>
