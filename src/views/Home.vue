<template>
    <div>
      <Banner :src="banner" :alt="bannerl"/>
      <div class="main-container">
        <h1>Monte o seu burger:</h1>

        <BurgerForm />
      </div>
    </div>
  </template>
  
  <script>
  import Banner from '../components/Banner'
  import BurgerForm from '../components/BurgerForm'
  
  export default {
    name: 'Home',
    components: {
      Banner,
      BurgerForm
    },
    data(){
        return{
            banner: "/img/burger.jpg",
            bannerl: "banner"
        }
    }
  }
  </script>