<template>
  <header>
  <Header/>
  </header>
  <router-view/>


<footer class="mt-[300px]" >
<Footer/>
</footer>
</template>
<script>
import Footer from './components/Layout/Footer.vue';
import Header from './components/Layout/Header.vue';
export default{
  components:{Header,Footer}
}



</script>

