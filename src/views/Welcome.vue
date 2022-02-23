<template>
    <div id="v-welcome" class="v-comp flex one center">
<h1>Benviungut/guda a la calculadora de pressupostos</h1>
<h2>Quins serveis necessites?</h2>
<p>Amb aquesta calculadora podreu obtenir un pressupost de tallat dels serveis que demaneu</p>

<div class="f-group">
       <router-link to="/home" class="button">Obre l'aplicació</router-link>
</div>
    </div>



</template>


<script>
export default ({
      name: "Welcome"
})
</script>

<style>
#v-welcome {
    display: flex;
    align-items: center;
    min-height: 25vh;
    align-content: center;
}
</style>
