<template>
  <div class="products-new">
    
      <h1>New Product</h1>
      <ul>
        <li v-for="error in errors">{{ error }} </li>
      </ul>

      <form v-on:submit.prevent="submit()">
  

        <div>
          Name: <input type="text" v-model="newProductName">
        </div>

        <div>
          Price: <input type="decimal" v-model="newProductPrice">
        </div>

        <div>
          Description: <input type="text" v-model="newProductDescription">
        </div>

        <div>
          Image_URL: <input type="text" v-model="newProductImageUrl">
        </div>

        <input type="submit" value="Create">


      </form>
    </div> 
</template>


<style>

</style>


<script>
var axios = require("axios");

export default {
  data: function() {
    return {
      products: [],
      errors: [],
      newProductName: "",
      newProductPrice: "", 
      newProductDescription: "",
      newProductImageUrl: "",
      currentProduct: {}
    };
  },
  created: function() {},
  methods: {
    submit: function() {
      console.log("Create the product...");

      var clientParams = {
      
        name: this.newProductName,
        price: this.newProductPrice,
        description: this.newProductDescription,
        image_url: this.newProductImageUrl

      }; 


      axios
        .post("/api/products", clientParams)
        .then(response =>{
          this.$router.push("/")
        })
        .catch(error => {
          this.errors = error.response.data.errors; 
        });
        

    }
  }
};
</script>