<script setup>
import { ref } from 'vue';
const header= ref('Mi carrito de compras')
const items = ref({
  "item1": { id: 1, label: '10 bolillos' },
  "item2": { id: 2, label: '1 lata de frijoles' },
  "item3": { id: 3, label: '2 lata de atún' },
});
const newItem= ref('1 Bolsa 🛍️💰');
const newItemHighPriority = ref("false");
</script>

<template>
    <h1> <i class="material-icons shopping-cart-icon">local_mall</i> {{ header }}</h1>
<h1></h1>
<div class="add-item form">
  <!--Input de nuevo articulo-->
  <input v-model.trim="newItem" type="text" placeholder="Ingresar articulo">
  <!-- Chek Boxes -->
  <label>
    <input v-model="newItemHighPriority" type="checkbox">
    Alta prioridad
  </label>
  {{ newItemHighPriority === "high" ?"🔥" :"🧊"}}
  <!--Boton de UI-->
  <boton v-on:click="items.push({id: items.length + 1, label: newItem}) " class="btn btn-primary">Salvar articulo</boton>
</div>
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
