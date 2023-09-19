<template>
  <div>
    <table>
      <th>
        <td>ID</td>
        <td>Title</td>
        <td>Desc</td>
        <td>Image</td>
        <td>Price</td>
        <td>Rating</td>
        <td>Category</td>
      </th>
      <!-- <tr v-for="(item,index) in dataWomen" :key="index">
        <td>{{ item }}</td> -->
        <!-- <td>{{ item.title }}</td>
        <td>{{ item. }}</td>
        <td>{{ item. }}</td>
        <td>{{ item. }}</td>
        <td>{{ item. }}</td>
        <td>{{ item. }}</td> -->
      <!-- </tr> -->
    </table>
  </div>
  <div>
    {{ dataWomen[index] }} <br> <br>
    <h1>Index Product ke : {{ index }}</h1>
  </div> <br> <br>
  <button @click="nextProduct">NEXT PRODUCT</button>
</template>

<script setup lang="ts">
import {onMounted, ref} from 'vue';

  interface Women{
    id:number;
    title: string;
    description: string;
    image: string;
    price: number;
    rating: number;
    category: string;
  }
  
  let dataWomen = ref<Women[]>([]);
  let index = ref(0);

  const getWomenClothing = async () => {
    const api = await fetch("https://fakestoreapi.com/products/category/women's clothing");
    const response = await api.json();
    return response;
  }

  getWomenClothing().then((res) =>{ 
        console.log(res)
        dataWomen.value = res;
    })

  const nextProduct = () => {
    index.value++;
    if(index.value > dataWomen.value.length - 1){
      index.value = 0;
    }
  }

  onMounted(() => {
      getWomenClothing();
  })

</script>

<style>

</style>