<template>
<header id="c-header">
 <img id="app-logo" alt="Vue logo" src="../assets/cercle.png" />
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
