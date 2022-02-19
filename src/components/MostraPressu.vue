<template>
<div id="c-MostraPressu">

<div v-if="currentPressu.length > 0" id="elPressu">

<h2>Pressupost Actual</h2>

<div v-html="renderPressu()"></div>

</div>
</div>

</template>

<script>
export default {

    name: "MostraPressu",
    props: ["currentPressu", "preuTotal"],
    data() {
        return {

        }
    },
    methods: {
    renderPressu() {
    let output = "";
    this.currentPressu.forEach((servei) => {
       output += servei.nom + ": " + servei.preu + "<br>";
    });
     //output += "Serveis Web: " + this.serveisweb[0].num + " idioma(s) i " + this.serveisweb[1].num + " pàgina(s)";
     output += "<br>";
     output += "Preu Total: " + this.preuTotal;
     return output
    }

    }



}
</script>

<style>
#elPressu {
    background: #FFF;
    height: 100%;
    margin: 0 22px 0 0;
}

</style>
