<template>
  <div class="rectangle-5" :class="{
      'gray-bg': notAvailable,
      'pink-bg': !notAvailable && (product && (product.category.toLowerCase() === 'women\'s clothing' || product.category.toLowerCase() === 'jewelery')),
      'blue-bg': product && (product.category.toLowerCase() === 'men\'s clothing' || product.category.toLowerCase() === 'electronics')
    }">
      <div class="rectangle-7">
        <div v-if="notAvailable" class="notAvailable">
          <div class="product-container">
            <div class="product-text">
              <br><br><br><br><br><br><br><br>
              <p style="text-align: center;">This product is unavailable to show</p>
              <div class="product-buttons">
                <button @click="getNextProduct" class="next-product-button">Next Product</button>
              </div>
            </div>
          </div>
        </div>
        <div v-else-if="loading" class="loader"> loading</div>
        <div v-else>
          <div class="product-container">
            <div class="product-image">
              <img :src="product ? product.image : ''" alt="Product Image" width="200" height="200">
            </div>
            <div class="product-text">
              <p class="product-title" :class="{
                'pink-text': product && (product.category.toLowerCase() === 'women\'s clothing' || product.category.toLowerCase() === 'jewelery'),
                'blue-text': product && (product.category.toLowerCase() === 'men\'s clothing' || product.category.toLowerCase() === 'electronics')
              }">{{ product ? product.title : '' }}</p>
              <div class="product-info">
                <p>{{ product ? product.category : '' }}</p>
                <hr>
                <p class="rating">{{ product ? product.rating.rate + '/5' : '' }}</p>
                <div class="rating-circles" :class="{
                  'pink-circles': product && (product.category.toLowerCase() === 'women\'s clothing' || product.category.toLowerCase() === 'jewelery'),
                  'blue-circles': product && (product.category.toLowerCase() === 'men\'s clothing' || product.category.toLowerCase() === 'electronics')
                }">
                  <span
                    v-for="index in 5"
                    :key="index"
                    class="rating-circle"
                    :class="{
                      'filled': product && index <= Math.floor(product.rating.rate),
                      'pink-filled': product && (product.category.toLowerCase() === 'women\'s clothing' || product.category.toLowerCase() === 'jewelery') && index <= Math.floor(product.rating.rate),
                      'blue-filled': product && (product.category.toLowerCase() === 'men\'s clothing' || product.category.toLowerCase() === 'electronics') && index <= Math.floor(product.rating.rate)
                    }"
                  ></span>
                </div>
              </div>
              <hr>
              <p>{{ product ? product.description : '' }}</p>
              <hr>
            <h2 class="price" :class="{
              'pink-text': (product && (product.category.toLowerCase() === 'women\'s clothing' || product.category.toLowerCase() === 'jewelery')) || false,
              'blue-text': (product && (product.category.toLowerCase() === 'men\'s clothing' || product.category.toLowerCase() === 'electronics')) || false
            }">{{ product ? `$${product.price}` : '' }}</h2>
              <div class="product-buttons" :class="{
                'pink-buttons': product && (product.category.toLowerCase() === 'women\'s clothing' || product.category.toLowerCase() === 'jewelery'),
                'blue-buttons': product && (product.category.toLowerCase() === 'men\'s clothing' || product.category.toLowerCase() === 'electronics')
              }">
                <button class="buy-button" :class="{
                  'pink-buy-button': product && (product.category.toLowerCase() === 'women\'s clothing' || product.category.toLowerCase() === 'jewelery'),
                  'blue-buy-button': product && (product.category.toLowerCase() === 'men\'s clothing' || product.category.toLowerCase() === 'electronics')
                }">Buy Now</button>
                <button @click="getNextProduct" :class="{
                  'pink-next-product-button': product && (product.category.toLowerCase() === 'women\'s clothing' || product.category.toLowerCase() === 'jewelery'),
                  'blue-next-product-button': product && (product.category.toLowerCase() === 'men\'s clothing' || product.category.toLowerCase() === 'electronics')
                }">Next Product</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        loading: true,
        currentIndex: 1,
        notAvailable: true,
        product: {},
      }
    },
    mounted() {
      this.getProduct();
    },
    methods: {
      getProduct() {
        if (this.currentIndex > 20) {
          this.notAvailable = true;
          this.loading = false;
        } else {
          this.loading = true;
          fetch(`https://fakestoreapi.com/products/${this.currentIndex}`)
            .then((response) => response.json())
            .then((data) => {
              this.notAvailable = false;
              this.product = data;
              this.loading = false;
            });
        }
      },
      getNextProduct() {
        this.currentIndex++;
        if (this.currentIndex == 22) {
          this.currentIndex = 1;
        }
        this.getProduct();
      }
    }
  }
  </script>
  
  
  <style scoped>
  .square {
    width: 1280px;
    height: 1832px;
    background: #fff;
  }
  .gray-bg {
    background: #D8D7D7;
  }
  .rectangle-7 {
    top: 85px;
    position: relative;
    max-width: 80%;
    height: auto;
    border-radius: 10px;
    background: #FFF;
    box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
    margin: 0;
    padding: 0;
  }
  
  .pink-text {
    color: #720060;
  }
  
  .blue-text {
    color: #002772;
  }
  
  .rating-circle {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    display: inline-block; 
    margin-right: 5px;
  
  }
  
  
  .rating-circle.pink-filled {
    background-color: #720060;
  }
  
  .rating-circle.blue-filled {
    background-color: #002772;
  }
  
  .body {
    margin: 0;
    padding: 0;
  }
  
    .rectangle-5 {
      min-height: auto; 
      max-width: 100%;
      display: flex;
      justify-content: center;
      align-items: stretch;
      position: relative; 
    }
  
  .product-info {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  .rating {
    margin: 0;
    text-align: right;
  }
  
  .product-container {
              display: flex;
              align-items: center;
  }
  
  .product-image {
    flex: 1;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .product-text {
    flex: 1;
    text-align: left;
    padding: 20px;
  }
  
  .rating {
    text-align: right;
  }
  
  .product-buttons {
    display: flex;
    justify-content: space-between; 
    width: 100%; 
  }
  
  .product-title {
              font-size: 20px;
              top: 50px;
            
  }
  
  .pink-text {
      color: #720060;
              border-color: #720060;
  }
  
  .blue-text {
      color: #002772;
              border-color: #002772;
  }
  
  .blue-bg {
    background: #D6E6FF;
  }
  .pink-bg {
    background: #FDE2FF;
  }
  .pink-buy-button {
    background-color: #720060;
  }
  .blue-buy-button {
    background-color: #002772;
  }
  
  .buy-button {
    color: #fff;
    padding: 10px 0;
    border: none;
    cursor: pointer;
    flex-grow: 1; 
    margin-right: 10px; 
  }
  .blue-next-product-button {
      background-color: #FFFF;
    color: #002772;
    padding: 10px 0; 
    cursor: pointer;
    border: 1px solid #002772;
    flex-grow: 1;
  }
  .pink-next-product-button {
        background-color: #FFFF;
    color: #720060;
    padding: 10px 0; 
    cursor: pointer;
    border: 1px solid #720060;
    flex-grow: 1;
  }
  .next-product-button {
    background-color: #FFFF;
    color: #1E1E1E;
    padding: 10px 0; 
    cursor: pointer;
    border: 1px solid #1E1E1E;
    flex-grow: 1;
  }
  
  </style>