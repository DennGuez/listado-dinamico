<script setup lang="ts">
import { ref } from 'vue';

interface Label {
  name: ''
}

/* V-model can't link to array, cuz need point a some name */
const productTags = ref<Label[]>([{ name: '' }])

const addProductTag = () => {
  if ( productTags.value.length === 5) return
  productTags.value.push({name: ''})
}

const onSubmit = () => {
/* turn from an array of objects to an array of strings */
  console.log(productTags.value.map(tag => tag.name ))
}

const deleteProductTag = ( index: number ) => {
  if( productTags.value.length === 1) {
    // productTags.value = [ { name: ''}]
    productTags.value[0] = { name: ''}
    return
  }
  productTags.value.splice( index, 1)
}

</script>

<template>
  <h3>Agregar hasta 5 etiquetas</h3>
  <div class="container">
    <div v-for="tag, index in productTags" class="row">
      <button 
      @click="deleteProductTag(index)"
      >-</button>
      <input @keyup.enter="addProductTag" type="text" :placeholder="index.toString()" v-model="tag.name">
      <button 
        v-if="index === (productTags.length - 1)"
        @click="addProductTag"
      >+</button>
    </div>
    <button @click="onSubmit()" >Submit</button>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.row {
  display: flex;
  margin-bottom: 5px;
}

button {
  margin-right: 5px;
  margin-left: 5px;
}
</style>
