<template>
    <div class="container">
      <div class="row">
        <div class="col-12 text-center">
          <h3 class="pt-3">Categories</h3>
        </div>
      </div>
      <div class="row">
        <div v-for="category of categories" :key="category.id" class="col-md-6 col-xl-4 col-12 pt-3  justify-content-around d-flex">
          <CategoryBox :category="category"></CategoryBox>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import CategoryBox from '../../components/Category/CategoryBox';
  var axios =  require('axios');
  export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: "Category",
    components : {CategoryBox},
    data() {
      return {
        baseURL : "//localhost:8080/",
        categories : null,
      }
    },
    methods: {
      async getCategories() {
        await axios.get(this.baseURL + "category/")
        .then(res => this.categories = res.data)
        .catch(err => console.log(err))
      }
    },
    mounted(){
      this.getCategories();
    }
  }
  </script>
  
  <style scoped>
  h4 {
    font-family: 'Roboto', sans-serif;
    color: #484848;
    font-weight: 700;
  }
  </style>