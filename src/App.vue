<script setup>
import { ref, computed } from 'vue';
// Creando una propiedad computada
const characterCount = computed(()=>{
  // Toda propiedad computada debe regresar un valor
  return newItem.value.length;
});
// Creando propiedad computada que invierte items de la lista
const reversedItems = computed(() => {
  return [...items.value].reverse(); 
});
const header = ref('App Lista de compras');
const items = ref([
  {id: 1, label: '10 bolillos',purchased:true,highPriority:false},
  {id: 2, label: '1 lata de frijoles',purchased:false,highPriority:true},
  {id: 3, label: '2 lata de atún',purchased:true,highPriority:false}
]);
//Funcion que altera el estado de compra de un item
const togglePurchesed=(item)=>{
  //Invertir la propiedad purches
  item.purchased=!item.purchased;
  }
//Agregando todo para giardar nuevo articulo
const saveItem = () => { 
// codigo para verificar si newItem no está vacío antes de agregarlo a la lista 
if (newItem.value.trim() !== '') { 
  items.value.push({ id: items.value.length + 1, label: newItem.value }); 
  // Borrar o limpiar la caja de texto de newItem 
  newItem.value = ''; 
} 
}; 
const newItem = ref('');
const newItemHighPriority = ref(false);
const habilitarFormulario =ref (false);
//Creo la nueva variable
const DoEdit=(edit)=>{
  //Le coloco la accion de que sea igual a un valor 
  habilitarFormulario.value=edit;
  //Le coloco la accion de borrar la caja de texto
  newItem.value="";
};
</script>
<template>
  <div class="header">
    <h1> <i class="material-icons shopping-cart-icon">local_mall</i> {{ header }}</h1>
  <button  v-if ="!habilitarFormulario" @click= "DoEdit(true)" class="btn btn-primary">Agregar articulo</button>
  <button  v-else @click= "DoEdit(false)" class="btn">Cancelar</button>
  </div>
  <!--  Esto se usa para crear un ipervinculo con una imagen dependiendo de lo que escribas en la 
    caja de texto
  <a :href="newItem">
  <i class="material-icons shopping-cart-icon">school</i>
</a>-->
  <form v-if="habilitarFormulario" v-on:submit.prevent="saveItem" class="add-item form">
    <!-- Input de Nuevo Articulo -->
    <input  v-model.trim="newItem" type="text" placeholder="Ingresar nuevo articulo">
    <!-- Check Boxes -->
    <label>
      <input  v-model="newItemHighPriority" 
      type="checkbox">
      Alta Prioridad
    </label>
    {{ newItemHighPriority ? "🔥" : "🧊" }}
    <!-- Boton de UI -->
    <button :disable="newItem.lenggth ==0" class="btn btn-primary">Salvar Articulo</button>
  <!-- Contador -->
  <p class="counter">
    {{ characterCount }} / 200
  </p>
  </form>
  <ul>
    <li v-for="({ id,label, purchased,highPriority },index) in reversedItems" 
    v-bind:key="id"
      :class="{strikeout :purchased,priority:highPriority}" 
      @click="togglePurchesed(reversedItems[index])"
      >
      ♥  {{ label }}
    </li>
  </ul>
  <p v-if="items.length==0">🌹Lista de compras vacia🥀</p>

</template>

<style scoped>
.shopping-cart-icon {
  font-size: 2rem; 
}
</style>
