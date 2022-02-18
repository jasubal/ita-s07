<template>
    <div id="v-welcome" class="v-comp flex one center">
<h1>Benviungut/guda a la calculadora de pressupostos</h1>
<p>Amb aquesta calculadora podreu obtenir un pressupost de tallat dels serveis que demaneu</p>
    </div>
    <button> <router-link to="/home" class="button">Obre l'aplicació</router-link></button>

</template>


<script>
export default ({
      name: "Wellcome"
})
</script>

<style>
#v-welcome {
    align-items: center;
    min-height: 25vh;
}
</style>
