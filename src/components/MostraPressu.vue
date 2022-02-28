<template>
  <div id="c-mostraPressu" class="c-modul">
    <div v-if="preuTotal > 1" id="elPressu">
      <h2>Pressupost Actual</h2>
      <div id="dadesPressu" v-html="renderPressu()"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MostraPressu",
  props: ["currentPressu", "preuTotal"],
  data() {
    return {};
  },
  methods: {
    renderPressu() {
      let output = "";
      let resum = this.currentPressu[0];

      output += '<h3 class="tit">Resum</h3>';
      output += "Data: " + resum.date + "</br>";
      resum.nomPressu !== ""
      ? (output += "Nom pressupost: " + resum.nomPressu + "</br>") : 0;
      resum.nomClient !== ""
      ? (output += "Client: " + resum.nomClient + "</br>") : 0;

      output += '<h3 class="tit">Productes</h3>';
      this.currentPressu.forEach((servei, idx) => {
      if (idx > 0) {
          if (servei.langs > 0) {
            //let totalServeisWeb = servei.langs * servei.pags * 30;
            output += servei.servei + ": " + servei.preu + "€<br>";
            output += servei.langs + " idioma/es + " + servei.pags + " pàgina/es : " + resum.totalServeisWeb + "€<br>";
          } else { output += servei.servei + ": " + servei.preu + "€<br>"; }
        }
      });
      output += "<br>";
      output += "<strong>Preu Total: " + resum.preuTotal + "€</strong></br>";

      return output;
    },
  },
};
</script>

<style scoped>
#c-mostraPressu {
  padding: 0;
}
#elPressu {
  height: 100%;
  margin: 0;
}
#dadesPressu {
  text-align: left;
  padding: 0 3em;
}
@media (min-width: 56.25em) {
#dadesPressu {
  text-align: left;
  padding: 0 2em;
}
}

@media (min-width: 75em) {

 }
</style>
