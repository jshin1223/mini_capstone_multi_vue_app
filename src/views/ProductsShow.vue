<template>
  <div class="products-show">
    <h1>{{ product.name }}</h1>
    <h5>Price: {{ product.formatted.price }}</h5>

    <h5>Description: {{ product.description }} </h5>

    <img v-bind:src="product.image_url" v-bind:alt="product.name">

    <div>
      <router-link v-bind:to=" '/products/' + product.id + '/edit' ">Edit</router-link>
      <button v-on:click="destroyProduct()">Destroy</button>
    </div>




  </div>
</template>

<style>
</style>





<script>
var axios = require('axios');



export default {
  data: function() {
    return {
      product: {
        id: "", 
        name: "", 
        price: "",
        description: "",
        image_url: "", 
        formatted: {
                   price: "",
                   tax: "",
                   total: "" 
        }
      }
    };
  },
  created: function() {
    axios
      .get("/api/products/" + this.$route.params.id)
      .then(response => {
        this.product = response.data; 

      });

  },
  methods: {

      destroyProduct: function() {
      axios
        .delete("/api/products/" + this.product.id)
        .then(response => {
          this.$router.push("/");  

        }); 
    }
  } 
};
</script>