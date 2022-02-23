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
      resum.nomPressu !== ""
        ? (output += "Nom pressupost: " + resum.nomPressu + "</br>")
        : 0;
      resum.nomClient !== ""
        ? (output += "Client: " + resum.nomClient + "</br>")
        : 0;
      output += "Data pressupost: " + resum.dataPressu + "</br>";

      output += '<h3 class="tit">Productes</h3>';

      this.currentPressu.forEach((item, index) => {
        if (index > 0) {
          if (item.langs > 0) {
            let totalServeisWeb = item.langs * item.pags * 30;
            output += item.servei + ": " + item.preu + "€<br>";
            output += item.langs + " idioma/es + " + item.pags + " pàgina/es : " + totalServeisWeb + "€<br>";
          } else { output += item.servei + ": " + item.preu + "€<br>"; }
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
  padding: 0 2em;
}
</style>
