
<template>
  <div class="container">
    <div class="btn-left">
      <button @click="prevProduct">
        <svg fill="none" viewBox="8 5 10 12" height="2em" width="1em">
          <path
            fill="currentColor"
            d="M16.243 6.343L14.828 4.93 7.758 12l7.07 7.071 1.415-1.414L10.586 12l5.657-5.657z"
          />
        </svg>
      </button>
    </div>

    <template v-if="!isLoading && !dataProduct[index].category.includes('clothing')">
      <unvailable-product/>
    </template>

    <template v-if="isLoading">
      <!-- <center> <h4>Please, Waiting until loading finished!</h4></center> -->
      <loading-screen/>
    </template>

    <div v-if="!isLoading && dataProduct[index].category.includes('clothing')" class="productCard">

      <div class="img">
        <img :src="dataProduct[index]?.image" :alt="dataProduct[index]?.title">
      </div>

      <div class="productDetail">

        <h2 class="title">{{ dataProduct[index]?.title }}</h2>

        <div class="category">
          <p>{{ dataProduct[index]?.category }}</p>
          <div class="testimonies">
            <ul>
              <!-- <li v-for="star in (Math.floor(dataProduct[index].rating.rate))" :key="star"> -->
            
              <li v-for="star in starsFilled" :key="star">
                <img src="/star_filled.png" alt="star-image">
              </li>
              <!-- <li v-if="dataProduct[index].rating.rate < 5" v-for="star in starsEmpty()" :key="star"> -->
              <li v-for="star in starsEmpty" :key="star">
                <img src="/start_empty.png" alt="star-image-empty">
              </li>
            </ul>
            <p>{{ dataProduct[index]?.rating.rate }}/5</p>
            <span>
              <img src="/reviews.png" alt="">
              <p>{{ dataProduct[index]?.rating.count }}</p>
            </span>
          </div>
        </div>
        <hr>
        <p class="description">
          <!-- {{ dataProduct[index].description.substring(0,250) }}... -->
          {{ dataProduct[index]?.description }}
        </p>
        <hr>
        <h2>${{ dataProduct[index]?.price }}</h2>
        <div class="btn">
          <!-- <button class="buyNow"  @click="prevProduct">Buy Now</button> -->
          <button class="buyNow">Buy Now</button>
          <button class="share">
            <svg
              viewBox="0 0 800 1000"
              fill="currentColor"
              height="1em"
              width="1em"
            >
              <path d="M650 650c41.333 0 76.667 14.333 106 43s44 64.333 44 107c0 41.333-14.667 76.667-44 106s-64.667 44-106 44-76.667-14.667-106-44-44-64.667-44-106c0-4 .333-8.667 1-14s1-9.333 1-12L242 618c-28 21.333-58.667 32-92 32-41.333 0-76.667-14.667-106-44S0 541.333 0 500s14.667-76.667 44-106 64.667-44 106-44c36 0 66.667 10 92 30l260-156c0-2.667-.333-6.667-1-12s-1-9.333-1-12c0-41.333 14.667-76.667 44-106s64.667-44 106-44 76.667 14.333 106 43 44 64.333 44 107c0 41.333-14.667 76.667-44 106s-64.667 44-106 44c-34.667 0-64.667-10.667-90-32L298 474c1.333 5.333 2 14 2 26 0 10.667-.667 18.667-2 24l262 156c24-20 54-30 90-30" />
            </svg>
          </button>
        </div>
      </div>
    </div>

    <div class="btn-left" @click="nextProduct">
      <button>
        <svg fill="none" viewBox="8 5 10 12" height="2em" width="1em">
          <path
            fill="currentColor"
            d="M10.586 6.343L12 4.93 19.071 12 12 19.071l-1.414-1.414L16.243 12l-5.657-5.657z"
          />
        </svg>
      </button>
    </div>

  </div>
  <!-- <div>
    <br> <br>
    {{ dataWomen[index] }} <br> <br>
    <h1>Index Product ke : {{ index }}</h1>
  </div>
  <button @click="nextProduct">NEXT PRODUCT</button> -->
</template>

<script setup lang="ts">
  import {onMounted, ref, computed} from 'vue';
  import LoadingScreen from './LoadingScreen.vue';
  import UnvailableProduct from './UnvailableProduct.vue';

  interface Product{
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
  
  const dataProduct = ref<Product[]>([]);
  const index = ref<number>(0);
  const isLoading = ref<boolean>(true);

  const getDataClothing = async () => {
    const api = await fetch("https://fakestoreapi.com/products/");
    const response = await api.json();
    // isLoading.value = false;
    return response;
  }

  getDataClothing().then((res) =>{ 
        console.log(res)
        dataProduct.value = res;
    })

  const nextProduct = () => {
    isLoading.value = true;
    setTimeout(() => {
      index.value++;
      if(index.value > dataProduct.value.length - 1){
        index.value = 0;
      }
      isLoading.value = false;
    }, 1000)
  }

  const prevProduct = () => {
    isLoading.value = true;
    setTimeout(() => {
      index.value--;
      if(index.value < 0){
        index.value = dataProduct.value.length - 1;
      }
      isLoading.value = false;
    }, 1000)
  }

  // const data = reactive(dataProduct.value[index.value].rating)
  // console.log(data)

  // const starsFilled = computed(() =>{
  //   return Math.floor(dataProduct.value[index.value].rating?.rate);
  // })

  const starsFilled = computed(() =>{
    return Math.floor(dataProduct.value[index.value].rating.rate);
  })

  const starsEmpty = computed(() =>{
    if(Math.floor(dataProduct.value[index.value].rating.rate) < 5){
      return 5 - Math.floor(dataProduct.value[index.value].rating.rate);
    }
  })

  onMounted(() => {
    getDataClothing();
  })

</script>
  
<style scoped>
  .container {
    display: flex;
    align-items: center;
    padding: 20px 30px;
    width: 95%;
    height: 500px;
    margin: 0 auto;
    border-radius: 0.45em;
    box-shadow: 0 2.8px 2.2px rgba(0, 0, 0, 0.034),
    0 6.7px 5.3px rgba(0, 0, 0, 0.048), 0 12.5px 10px rgba(0, 0, 0, 0.06),
    0 22.3px 17.9px rgba(0, 0, 0, 0.072), 0 41.8px 33.4px rgba(0, 0, 0, 0.086),
    0 100px 80px rgba(0, 0, 0, 0.12);
    position: relative;
  }
  .productCard{
    justify-content: center;
    align-items: center;
    width: 100%;
    display: flex;
    gap: 50px;
  }
  .productCard .img{
    width: 35%;
  }
  .productCard img{
    width: 320px;
    height: 400px; 
  }

  .productDetail{
    width: 65%;
    height: 460px;
    text-align: left;
  }
  .productDetail .category{
    display: flex;
    justify-content: space-between;
  }

  .testimonies{
    display: flex;
    gap: 5px;
  }
  .testimonies ul{
    display: flex;
  }
  .testimonies ul li{
    list-style: none;
  }
  .testimonies img{
    width: 20px;
    height: 20px;
  }
  .testimonies span{
    display: flex;
    align-items: center;
    gap: 6px;
    margin-left: 10px;
  }
  .title{
    line-height: 30px;
    height: 40px;
  }
  .description{
    width: 95%;
    height: 110px;
    overflow: hidden;
  }

  .btn {
    display: flex;
    gap: 20px;
  }
  .btn .buyNow {
    width: 300px;
  }
  .btn .share {
    width: 80px;
  }
</style>