<template>
  <li>{{ item.name }}
    <button @click="addToCart(item.id)">Add</button>
  </li>
</template>¨

<script  lang="ts">
import Vue from 'vue';

type Item = { id: number, name: string, quantity: number }

export default Vue.extend({
  name: 'ShopItem',
  props: {
    item: {
      type: Object as () => Item,
      required: true
    }
  },
  methods: {
    addToCart(itemId: number) {
      this.$emit('add-to-cart', itemId);
    }
  }
});
</script>

<style scoped>
li {
  list-style-type: none;
}

button {
  background: transparent;
  border: none;
  background-color: lightgreen;
}

button:hover {
  background-color: green;
}

button:active {
  outline: none;
  border: none;
  background-color: rgb(255, 255, 255);
  color: black;
}
</style>
