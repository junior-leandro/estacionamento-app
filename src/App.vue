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



<style> /* O Style sem 'scoped altera todos os componentes */

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;
}

.main-container{
    margin: 40px;
    min-height: 75vh;
  }
  h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 40px;
  }

</style>
