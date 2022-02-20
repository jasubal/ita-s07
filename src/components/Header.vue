<template>
<header id="c-header">
    <div id="app-brand">
 <img id="app-logo"  alt="Vue logo" src="../assets/cercle.png" />
 <h1>Calculadora de Pessupostos</h1>
    </div>

 <div id="nav">
      <router-link to="/">Welcome</router-link> |
      <router-link to="/home">Home</router-link> |
      <router-link to="/about">About</router-link>
  </div>
</header>
</template>

<script>
export default {
    name: 'Header',
}

</script>

<style>

</style>
