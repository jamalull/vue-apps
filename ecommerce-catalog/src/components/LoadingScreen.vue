<template>
  <div class="productCard">

    <div class="img">
      <div></div>
    </div>

    <div class="productDetail">

      <!-- <h2 class="title">{{ dataWomen[index]?.title }}</h2> -->
      <!-- <h2 class="title">Title</h2> -->
      <div class="title"></div>

      <div class="category">
        <!-- <p>{{ dataWomen[index]?.category }}</p> -->
        <!-- <p>Category</p> -->
        <div class="testimonies">
          <ul>
            <!-- <li v-for="star in (Math.floor(dataWomen[index].rating.rate))" :key="star"> -->
          
          </ul>
          <!-- <p>{{ dataWomen[index]?.rating.rate }}/5</p> -->
          <!-- <p>4.7/5</p> -->
          <span>
            <!-- <img src="/reviews.png" alt=""> -->
            <!-- <p>{{ dataWomen[index]?.rating.count }}</p> --> 
          </span>
        </div>
      </div>
      <hr>
      <p class="description">
        <!-- {{ dataWomen[index].description.substring(0,250) }}... -->
        <!-- {{ dataWomen[index]?.description }} -->
        
      </p>
      <hr>
      <!-- <h2>${{ dataWomen[index]?.price }}</h2> -->
      <div class="price"></div>
      <div class="btn">
        
        <p></p>
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
</template>

<script setup lang="ts">
  

</script>

<style scoped>
  .productCard{
    justify-content: center;
    align-items: center;
    width: 100%;
    display: flex;
    gap: 50px;
    margin: 0 20px;
  }
  .productCard .img{
    width: 35%;
    margin: 0 20px;
    /* height: 400px;  */
  }
  .productCard .img div{
    background-color: #d5e3e560;
    width: 320px;
    height: 400px; 
  }

  .productDetail{
    width: 100%;
    height: 460px;
    text-align: left;
  }
  .productDetail .category{
    width: 100%;
    margin-top: 5px;
    background-color: #d5e3e560;
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
  .productDetail .title{
    background-color: #d5e3e560;
    /* width: 100%; */
    height: 40px;
  }
  .description{
    background-color: #d5e3e560;
    width: 95%;
    height: 110px;
    overflow: hidden;
  }
  .price{
    background-color: #d5e3e560;
    width: 20%;
    height: 40px;
    margin-bottom: 10px;
  }

  .btn {
    display: flex;
    gap: 20px;
    /* background-color: #d5e3e560;
    width: 50%;
    height: 40px; */
  }
  .btn .buyNow {
    width: 300px;
  }
  .btn .share {
    width: 80px;
  }
</style>