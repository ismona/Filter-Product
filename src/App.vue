<template>
  <h1>#product-finder</h1>
  <filter-form @pass-data="loadFilteredData"></filter-form>
  <product-card :products="products"></product-card>
</template>

<script>
import axios from "axios";
import FilterForm from "./components/FilterForm.vue";
import ProductCard from "./components/ProductCard.vue";

export default {
  name: "App",
  components: {
    FilterForm,
    ProductCard,
  },
  data () {
    return {
      products: []
    }
  },
  methods: {
    loadFilteredData(selectedCompany){
      axios
        .get("http://fake-api.ns.nsdevel.eu/products")
        .then((resp3) => {
          this.products = resp3.data.products.filter(
            (product) => product.company.name === selectedCompany
          );
        })
        .catch((error) => {
          console.error("There was an error!", error);
        });
    },
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
h1 {
  color: #616060;
  font-size: 40px;
  text-align: center;
  margin: 0px 0px 30px;
}
#app {
  font-family: "Merriweather", serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: #f6f6f6;
  padding-top: 40px;
}
</style>
