<template>
  <div>
    <div class="productCard">
      <img :src="dataWomen[index].image" :alt="dataWomen[index].title">
      <div class="productDetail">
        <h2 class="title">{{ dataWomen[index].title }}</h2>
        <div class="category">
          <p>{{ dataWomen[index].category }}</p>
          <p>{{ dataWomen[index].rating.rate }}/5</p>
        </div>
        <hr>
        <p class="description">
          {{ dataWomen[index].description }}
        </p>
        <hr>
        <h2>${{ dataWomen[index].price }}</h2>
        <div class="btn">
          <button class="buyNow">Buy Now</button>
          <button class="nextProduct" @click="nextProduct">Next Product</button>
        </div>
      </div>
    </div>
  </div>
  <div>
    <br> <br>
    {{ dataWomen[index] }} <br> <br>
    <h1>Index Product ke : {{ index }}</h1>
  </div> <br> <br>
  <button @click="nextProduct">NEXT PRODUCT</button>
</template>

<script setup lang="ts">
  import {onMounted, ref} from 'vue';

  interface Women{
    id:number,
    title: string,
    description: string,
    image: string,
    price: number,
    rating: {
      rate:number,
      count:number
    },
    category: string
  }
  
  const dataWomen = ref<Women[]>([]);
  const index = ref(0);

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
  .productCard{
    display: flex;
    gap: 50px;
  }
  .productCard img {
    width: 315px;
    height: 400px; 
  }

  .productDetail{
    text-align: left;
  }
  .productDetail .category{
    display: flex;
    justify-content: space-between;
  }

  .btn {
    display: flex;
    gap: 30px;
  }
  .btn button {
    width: 300px;
  }
</style>