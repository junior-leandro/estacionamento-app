<template>
  <Navbar :logo="logo_src" :alt="app_name"/>

  <RouterView /> <!-- AS views-->

  <Footer />
</template>



<script>
import Navbar from './components/Navbar.vue';
import Footer from './components/Footer.vue';

export default {

  components: {
    Navbar,
    Footer,
  },

  data() {
    return{
      logo_src: "/img/carro.png",
      app_name: "Cadastre o carro no estacionamento"
    }
  }
}
</script>



<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;
}



</style>
