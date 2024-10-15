<script>
  import Formulario from './components/Formulario.vue';
  import Header from './components/Header.vue';
  import Footer from './components/Footer.vue';
  export default{
    components:{
      Header,
      Formulario,
      Footer
    }
  }
</script>

<template>
  <Header/>
  <main>
    <Formulario/>
  </main>
  <Footer/>
</template>

<style scoped>
</style>
