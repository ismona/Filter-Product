<template>
  <form>
    <div id="filter">
      <div class="select-arrow">
        <select v-model="selectedCompany">
          <option disabled value="">Značka produktu...</option>
          <option
            v-for="company in companies"
            :value="company.name"
            :key="company.id"
            >{{ company.name }}</option
          >
        </select>
      </div>

      <div class="select-arrow">
        <select v-model="selectedCategory">
          <option disabled value="">Kategoria produktu...</option>
          <option
            v-for="category in categories"
            :value="category.id"
            :key="category.id"
            >{{ category.name }}</option
          >
        </select>
      </div>
    </div>
    <button @click.prevent="filterProducts(selectedCompany)">
      <svg
        width="64"
        height="64"
        viewBox="0 0 64 64"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <g filter="url(#filter0_d)">
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M35.1901 33.4782L41.6458 39.934C41.8727 40.1611 42.0001 40.469 42 40.79C41.9999 41.111 41.8723 41.4189 41.6452 41.6458C41.4181 41.8727 41.1102 42.0001 40.7892 42C40.4682 41.9999 40.1604 41.8723 39.9335 41.6452L33.4778 35.1893C31.5479 36.6841 29.1211 37.3875 26.691 37.1565C24.261 36.9255 22.0102 35.7773 20.3966 33.9457C18.7829 32.114 17.9277 29.7364 18.0048 27.2965C18.0819 24.8567 19.0856 22.5378 20.8116 20.8117C22.5377 19.0856 24.8565 18.0819 27.2963 18.0048C29.7361 17.9277 32.1137 18.783 33.9453 20.3966C35.7769 22.0103 36.925 24.2611 37.156 26.6913C37.387 29.1214 36.6836 31.5483 35.1889 33.4782H35.1901ZM27.6004 34.7993C29.5099 34.7993 31.3412 34.0408 32.6914 32.6905C34.0416 31.3403 34.8001 29.509 34.8001 27.5995C34.8001 25.69 34.0416 23.8587 32.6914 22.5084C31.3412 21.1582 29.5099 20.3996 27.6004 20.3996C25.691 20.3996 23.8597 21.1582 22.5095 22.5084C21.1593 23.8587 20.4008 25.69 20.4008 27.5995C20.4008 29.509 21.1593 31.3403 22.5095 32.6905C23.8597 34.0408 25.691 34.7993 27.6004 34.7993Z"
            fill="white"
          />
        </g>
        <defs>
          <filter
            id="filter0_d"
            x="0"
            y="0"
            width="64"
            height="64"
            filterUnits="userSpaceOnUse"
            color-interpolation-filters="sRGB"
          >
            <feFlood flood-opacity="0" result="BackgroundImageFix" />
            <feColorMatrix
              in="SourceAlpha"
              type="matrix"
              values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0"
              result="hardAlpha"
            />
            <feOffset dx="2" dy="2" />
            <feGaussianBlur stdDeviation="10" />
            <feComposite in2="hardAlpha" operator="out" />
            <feColorMatrix
              type="matrix"
              values="0 0 0 0 0.878431 0 0 0 0 0.878431 0 0 0 0 0.878431 0 0 0 0.6 0"
            />
            <feBlend
              mode="normal"
              in2="BackgroundImageFix"
              result="effect1_dropShadow"
            />
            <feBlend
              mode="normal"
              in="SourceGraphic"
              in2="effect1_dropShadow"
              result="shape"
            />
          </filter>
        </defs>
      </svg>
    </button>
  </form>

</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      companies: [],
      selectedCompany: "",
      categories: [],
      selectedCategory: ""
    };
  },
  mounted() {
    this.getProducts();
  },
  methods: {
    getProducts() {
      axios
        .all([
          axios.get("http://fake-api.ns.nsdevel.eu/companies"),
          axios.get("http://fake-api.ns.nsdevel.eu/categories"),
        ])
        .then(
          axios.spread((resp1, resp2) => {
            this.companies = resp1.data.companies;
            this.categories = resp2.data.categories;
          })
        );
    },
    filterProducts(selectedCompany, selectedCategory) {
      this.$emit('pass-data', selectedCompany, selectedCategory);
      console.log(this.selectedCompany + '' + this.selectedCategory);
    },
  },
};
</script>

<style scoped>
select {
  all: initial;
  font-size: 19px;
  color: #616060;
  width: 300px;
  padding-left: 20px;
}
.select-arrow::after {
  content: "→";
}
.select-arrow {
  padding: 0px 20px;
}
#filter {
  display: block;
  min-height: 60px;
  border: 1px solid #ebebeb;
  border-radius: 20px;
  background: #fff;
  display: flex;
  align-items: center;
}
button {
  all: initial;
  background: #98c183;
  width: 97px;
  height: 60px;
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-left: 18px;
}
form {
  display: flex;
  justify-content: center;
}
</style>
