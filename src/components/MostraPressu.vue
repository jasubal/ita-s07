<template>
<div id="c-mostraPressu" class="c-modul">

<div v-if="preuTotal > 1 " id="elPressu">
<h2>Pressupost Actual</h2>
<div id="dadesPressu" v-html="renderPressu()"></div>
</div>
<!-- <pre>{{currentPressu}}</pre> -->
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
    let output = '';
    let resum = this.currentPressu[0].resum;
    let productes = this.currentPressu[1].productes;
    let dataActual = new Date().toLocaleDateString()
    output += '<h3 class="tit">Resum</h3>';
    output += 'Data pressupost: '+ dataActual + '</br>';
 (resum.nomClient !== '') ? (output += 'Client: ' + resum.nomClient + '</br>' ) : 0;
 (resum.nomPressu !== '') ? (output += 'Descripció: ' + resum.nomPressu + '</br>' ) : 0;
    output += '<h3 class="tit">Productes</h3>';
    productes.forEach((producte) => {
        if (producte.langs > 0 && producte.pags > 0) {
output += producte.nom + '<br>Idioma/es: ' + producte.langs + ' - Pàgina/es: '+  producte.pags + '<br>';
        } else {
    output += producte.nom + ':'+ producte.preu + '</br>';
        }
    });
    output += '<br>';
    output += 'Preu Total: ' + resum.preu + '</br>';
    /*
    this.currentPressu.forEach((item,index) => {
       currentPressu[0]
       //';
    });
    */
     //output += "Serveis Web: " + this.serveisweb[0].num + " idioma(s) i " + this.serveisweb[1].num + " pàgina(s)";

     return output
    }

    }



}
</script>

<style scoped>
#c-mostraPressu {
    padding: 0;
}
#elPressu {
    background: #FFF;
    height: 100%;
    margin: 0 22px 0 0;
}

#dadesPressu {
    text-align: left;
    padding: 0 2em;
}
#dadesPressu .tit{
    font-size: 1.2em;
    margin: 0;
    padding: 0.6em 0 0;
}
</style>
