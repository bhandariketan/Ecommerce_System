<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  
      <router-link class="navbar-brand" :to="{name : 'Home'}">
        <img id="logo" src="../assets/cig.png" />
      </router-link>
  
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent"
       aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent"></div>
  
      <ul class="nav justify-content-center">
        <li class="nav-item"><router-link class="nav-link" :to="{name : 'AdminCategory'}">Category</router-link></li>
        <li class="nav-item"><router-link class="nav-link" :to="{name : 'BrandCategory'}">Brands</router-link></li>
        <li class="nav-item"><router-link class="nav-link" :to="{name : 'AdminProduct'}">Products</router-link></li>
        <li class="nav-item dropdown">
          <a class="nav-link text-light dropdown-toggle" v-if="!userId" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
              Accounts
          </a>
          <a class="nav-link text-light dropdown-toggle" v-if="userId" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
            {{userName}}
          </a>
          <div class="dropdown-menu" aria-labelledby="navbarDropdown">
              <router-link class="dropdown-item" v-if="!userId" :to="{name: 'Login'}">Log In</router-link>
              <router-link class="dropdown-item" v-if="!userId" :to="{name: 'Register'}">Register</router-link>
              <router-link class="dropdown-item" v-if="admin" :to="{name: 'Analytics'}">Analytics</router-link>
              <a class="dropdown-item" v-if="userId" href="#" @click="signout">Sign Out</a>
          </div>
        </li>
        <li class="nav-item">
         <router-link class="text-light" v-if="userId" :to="{name : 'ShoppingCart'}"><i class="fa fa-shopping-cart" style="font-size:36px"></i></router-link>
        </li>
      </ul>
    </nav>
  </template>
  
  <script>
  import swal from 'sweetalert';
  export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name : "Navbar",
    data() {
        return {
          userId: null,
          userName: null,
          admin: null
        };
    },
    methods: {
        signout() {
            localStorage.removeItem('userId');
            localStorage.removeItem('userName');
            this.userId = null;
            this.userName = null;
            this.admin = null;
            this.$router.push({name:'Home'});
            swal({
                text: "Logged you out. Visit Again",
                icon: "success",
                closeOnClickOutside: false,
            });
        }
    },
    mounted() {
      this.userId = localStorage.getItem('userId');
      this.userName = localStorage.getItem('userName');
      if(this.userName=="admin"){
        this.admin = this.userName
      } 
    }
  }
  </script>
  
  <style scoped>
    #logo {
      width: 150px;
      margin-left: 20px;
      margin-right: 20px;
    }
  
    .nav-link {
      color: rgba(255,255,255);
    }
  
    #search-button-navbar {
      background-color: #febd69;
      border-color: #febd69;
      border-top-right-radius: 2px;
      border-bottom-right-radius: 2px;
    }

    .bg-dark {
    background-color: black !important;
    }

    .nav{
      margin-top: revert !important;
    }

  </style>
  