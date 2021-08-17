<template>
  <div class="container">
    <ul v-for="product in products" :key="product.id">
      <li>
        <div id="product-card">
          <img :src="product.images" alt="product-img" />
          <p>{{ product.images }}</p>
          <h2>{{ product.name }}</h2>
          <p class="company">{{ product.company.name }}</p>
          <div class="right">
            <p class="price">{{ product.price }} €</p>
            <p v-if="product.stock > 0" class="stock">Skladom</p>
            <p v-else class="no-stock">Nie je skladom</p>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    products: {
      type: Array,
      required: true,
    },
  },
  methods: {
    getImgUrl(img) {
      return require(`@/assets/${img}`);
    }
  }
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  align-items: center;
  margin: 0px 100px;
}
#product-card {
  border: 1px solid #ebebeb;
  max-width: 227px;
  background: #fff;
  width: 204px;
  height: 321px;
  border-radius: 20px;
  padding: 20px;
}
h2 {
  font-size: 18px;
}
.company {
  color: #616060;
  font-size: 12px;
  text-transform: uppercase;
  background: #fae9e1;
  border-radius: 5px;
  display: inline-block;
  padding: 5px 7px;
  font-family: "Roboto", sans-serif;
  margin: 0px;
}
.price {
  color: #9bc183;
  font-size: 24px;
  margin: 0px;
}
.stock,
.no-stock {
  font-family: "Roboto", sans-serif;
  font-size: 12px;
  text-transform: uppercase;
  color: #9bc183;
  margin: 0px;
}
.no-stock {
  color: #c18383;
}
ul {
  display: inline-block;
  padding-left: 0px;
}
li {
  list-style-type: none;
  padding: 10px 20px;
}
.right {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  margin-top: 20px;
}
</style>
