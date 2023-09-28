<script setup>
import { ref } from 'vue';
const header= ref('Mi carrito de compras')
const items = ref({
  "item1": { id: 1, label: '10 bolillos' },
  "item2": { id: 2, label: '1 lata de frijoles' },
  "item3": { id: 3, label: '2 lata de atún' },
});
</script>

<template>
  <h1>{{ header }}</h1>
  <ul>
    <li v-for="({ id, label }, index) in items" v-bind:key="id">
			♥ -{{ index }}- {{ label }}
		</li>
  </ul>
</template>

<style scoped>
.shopping-cart-icont{
  font-size: 2rem;
}
</style>
