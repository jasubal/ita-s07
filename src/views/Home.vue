
<script>
import Panell from "../components/Panell.vue";
import Alert from "../components/Alert.vue";
import MostraPressu from "../components/MostraPressu.vue";
import LlistaPressus from "../components/LlistaPressus.vue";


export default {
  name: "Home",
  components: { Panell, Alert, MostraPressu, LlistaPressus },
  data() {
    return {
      //urlQuery: '',
      nomClient: '',
      nomPressu: '',
      serveis: [
        { selected: false, servei: "Pàgina web", slug: "web", preu: 500,  langs: 1, pags: 1 },
        { selected: false, servei: "Consultoria SEO", slug: "seo", preu: 300 },
        { selected: false, servei: "Campanya de Publicitat", slug: "ads", preu: 400 },
      ],
      currentPressu: [],
      pressusList: [],
      showServeisweb: false,
      totalServeisWeb: 0,
      totalServeis: 0,
      preuTotal: 0,
      alert1: false,
      labAlert1: "Alerta",
      msgAlert1: "Emplena nom del client,<br> nom del pressupost<br> i un servei com a mínim",

    };
  },
  watch: {
    serveis: {
      handler: function () {
        this.calculaPreuTotal;
        this.updateUrl();
        },
      deep: true
    },
    nomClient: function () { this.calculaPreuTotal; },
    nomPressu: function () { this.calculaPreuTotal; },
  },
  created() {
    //console.log('dom Home created!');
    (Object.keys(this.$route.query).length !== 0) ? this.updateFromUrl() : this.updateCurrentPresu();
  },
   mounted() {
    //console.log('dom Home mounted!');
    this.$refs.nomClient.focus();
  },
  computed: {
    calculaPreuTotal: function(){
      const serveisPicked = this.serveis.filter((item) => item.selected===true);
      this.totalServeis = serveisPicked.reduce(
      (accumulator, currentItem) => { return accumulator + currentItem.preu; }, 0);
      this.showServeisweb ?
      this.totalServeisWeb = this.serveis[0].langs * this.serveis[0].pags * 30 : 0
      this.preuTotal = this.totalServeis + this.totalServeisWeb;
      this.updateCurrentPresu();
      return this.preuTotal;
      //console.log(this.preuTotal);
    },
  },
  methods: {
    updateCurrentPresu(option) {
      if (option === "clear") {
        this.currentPressu = [];
      } else {
      let dataAvui = this.getCurrentDateTime();
      let idPressu = this.getUniqueId();
      this.currentPressu = [];
      //this.calculaPreuTotal;
      this.currentPressu.push({
      id:idPressu, nomPressu:this.nomPressu, nomClient:this.nomClient, date:dataAvui, totalServeis:this.totalServeis,totalServeisWeb:this.totalServeisWeb, preuTotal:this.preuTotal, });
      this.serveis.map((servei) => { servei.selected ? this.currentPressu.push(servei) : 0 });
      //console.log(...this.currentPressu);
      }
    },
    check(e,idx) {
        if (this.serveis[0].selected== false) {
        this.serveis[0].langs = 1; this.serveis[0].pags = 1; this.totalServeisWeb = 0;
      }
      this.serveis[idx].selected = e.target.checked;
      //console.log("↓ chek/unchek ↓ ");
      //console.log(this.serveis[idx]);
      this.serveis[idx] === 0 ? this.showServeisweb = true : this.showServeisweb = false;
      this.showServeisweb = this.serveis[0].selected;
      this.calculaPreuTotal;
    },
    addPressu() {
      if (this.nomPressu === "" || this.nomClient === "" || this.preuTotal === 0) {
        this.alert1 = true;
      } else {
        // https://www.kuworking.com/javascript-como-copiar-arrays la copia con JSON
        const pressupost = JSON.parse(JSON.stringify(this.currentPressu))
        this.pressusList.push({ pressupost });
        this.resetForm();
      }
    },
    getUniqueId() {
      //return new Date().getTime();
      let uniqueId = window.crypto.getRandomValues(new Uint32Array(1))[0];
      return uniqueId.toString(16);
    },
    getCurrentDateTime() {
      let today = new Date();
      let date = today.getFullYear() + '-' + (today.getMonth() + 1) + '-' + today.getDate();
      let time = today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
      return date + ' ' + time;
    },
resetForm() {
  this.$router.push({path: '/home', query: {}});
  this.$refs.form.reset();
  this.nomClient = ''; this.nomPressu = '';
  this.serveis.map((servei) => { servei.selected = false; });
  this.serveis[0].langs = 1;
  this.serveis[0].pags = 1;
  this.showServeisweb = false;
  this.totalServeisWeb = 0;
  //this.totalServeis= 0;
  //this.showServeisweb = false;
  /*
  this.showServeisweb = false;
  this.serveis[0].selected = false;
  this.serveis[0].langs = false;
  this.serveis[0].pags = false;
  this.serveis[1].selected = false;
  this.serveis[2].selected = false;
  */

  },
updateFromUrl() {
//this.urlQuery = this.$route.query;
  this.serveis[0].selected = (this.$route.query.web === "true" ? true : false);
  this.$route.query.web === "true" ? this.showServeisweb = true : this.showServeisweb = false;
  if ( this.$route.query.web === "false") {
  this.serveis[0].langs = 1;
  this.serveis[0].pags = 1;
  this.totalServeisWeb = 0;
  } else {
      this.serveis[0].langs = this.$route.query.langs;
      this.serveis[0].pags = this.$route.query.pags;
  }
  this.serveis[0].pags = this.$route.query.pags;
  this.serveis[1].selected = (this.$route.query.seo === "true" ? true : false);
  this.serveis[2].selected = (this.$route.query.ads === "true" ? true : false);
},
updateUrl() {
this.$router.push({
  path: '/home', query: {
  web: this.serveis[0].selected, langs: this.serveis[0].langs, pags: this.serveis[0].pags,
  seo: this.serveis[1].selected,
  ads: this.serveis[2].selected,
  }
})
//this.urlQuery = this.$route.query;
    }
  },
  // end methods:

};
</script>

<template>
  <div id="v-home" class="maxW1300">
    <div id="ruta">{{  }}</div>

    <div id="c-formulari" class="flex one three-800 center">
      <MostraPressu :currentPressu="currentPressu" :preuTotal="preuTotal" />

      <form id="c-form" class="flex one center c-modul" ref="form">
        <h2>Calculadora de Pressupostos</h2>
        <div id="f-camps">
          <div class="f-group">
            <input type="text" v-model="nomClient" placeholder="Nom client" ref="nomClient" />
          </div>
          <div class="f-group">
            <input type="text" v-model="nomPressu" placeholder="Nom Pressupost" />
          </div>
          <div id="choose-serveis" class="f-group">
            <input
              id="check-pressu"
              type="checkbox"
              v-model="serveis[0].selected"
              value="true"
              @change="check($event, 0)"
            />
            <label for="check-pressu" class="checkable">Pàgina web (500€)</label>
            <div v-if="showServeisweb">
              <Panell :serveis="serveis" @serveis="serveis = $event" />
            </div>

            <input
              id="check-seo"
              type="checkbox"
              v-model="serveis[1].selected"
              value="true"
              @change="check($event, 1)"
            />
            <label for="check-seo" class="checkable">Consultoria SEO (300 €)</label>

            <input
              id="check-ads"
              type="checkbox"
              v-model="serveis[2].selected"
              value="true"
              @change="check($event, 2)"
            />
            <label for="check-ads" class="checkable">Campanya de Publicitat (400 €)</label>
          </div>

          <h3>Preu total: {{ preuTotal }} €</h3>
          <div class="f-group">
            <div v-if="alert1">
              <Alert :lab1="labAlert1" :msg="msgAlert1" @alert="alert1 = $event"></Alert>
            </div>
            <button @click="addPressu()">Guarda el Pressupost</button>
          </div>
        </div>
      </form>

      <LlistaPressus :pressusList="pressusList" />
    </div>
  </div>
</template>


<style scoped>
#ruta {color: red;}
#v-home {
  padding: 0;
}
#c-formulari {
  padding: 0;
}
h3 {
  margin: 0;
  padding: 0;
}
form {
  display: flex;
  align-content: flex-start;
}
input,
textarea {
  max-width: 18em;
  margin: 10px 0 0;
}
input[type="checkbox"] {
  width: 1em;
}
#choose-serveis {
  width: 100%;
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  align-content: center;
  align-items: flex-start;
}
label {
  margin: 10px 0;
  cursor: pointer;
}

@media (min-width: 56.25em) {
}

@media (min-width: 75em) {
}
</style>
