<script>
import Header    from './components/Header.vue'
//import Formulari from './components/Formulari.vue'
import Footer    from './components/Footer.vue'

export default {
  name: 'App',
  components: {Header,Footer }
}
</script>

<template>
<div id="page">
  <Header />
  <!-- component matched by the route will render here -->
  <div id="v-views" class="flex one center">
  <router-view />
  </div>

<Footer />
</div>
</template>



<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#v-views {
  min-height: 80vh;
}
</style>
