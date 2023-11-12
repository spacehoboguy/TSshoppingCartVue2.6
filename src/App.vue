<template>
  <div id="app">
    <HelloWorld :msg="title" />
    <div class="shop">
      <b>Store:</b>
      <ShopItem v-for="item in inventory" @add-to-cart="addToCart" :key="item.id" :item="item" />
    </div>
    <div class="cart">
      <b>Cart:</b>
      <div v-if="shoppingCart.length === 0"> No items</div>
      <div v-else>
        <li v-for="item in shoppingCart" :key="item.id" :item="item">{{ item.name }}</li>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import HelloWorld from './components/HelloWorld.vue';
import ShopItem from './components/ShopItem.vue';

let id = 0;
type Item = { id: number, name: string, quantity: number }

export default Vue.extend({
  name: 'App',
  components: {
    HelloWorld,
    ShopItem
  },
  data(): { inventory: Item[], shoppingCart: Item[], title: string } {
    return {
      inventory: [
        {
          id: id++, name: 'Orange', quantity: 1
        },
        {
          id: id++, name: 'Peach', quantity: 1
        },
        {
          id: id++, name: 'Kiwi', quantity: 1
        }
      ],
      shoppingCart: [
      ],
      title: 'Fruit Store'
    };
  },
  methods: {
    addToCart(itemId: number) {
      const item = this.inventory.find((i) => i.id === itemId);
      if (item) {
        this.shoppingCart.push(item);
        console.log('added item', item.name);
      } else {
        console.log('item not found');
      }
    }
  }

});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  /*
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px; */
}

.shop {
  width: 150px;
  height: 150px;
  border: 1px solid black;
}

.cart {
  width: 150px;
  height: 150px;
  border: 1px solid black;
  color: black;
}
</style>
