
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
      urlQuery: '',
      idPressu: '',
      nomClient: '',
      nomPressu: '',
      serveis: [
        { servei: "Pàgina web", slug: "web", preu: 500, selected: false, langs: 1, pags: 1, },
        { servei: "Consultoria SEO", slug: "seo", preu: 300, selected: false },
        { servei: "Campanya de Publicitat", slug: "ads", preu: 400, selected: false },
      ],
      serveisPicked: [],
      currentPressu: [],
      pressusList: [],
      pressusListLength: 0,
      totalServeis: 0,
      showServeisweb: false,
      totalServeisWeb: 0,
      preuTotal: 0,
      alert1: false,
      labAlert1: "Alerta",
      msgAlert1: "Emplena nom del client,<br> nom del pressupost<br> i un servei com a mínim",

    };
  },
  watch: {
    // '$route' (to, from) { this.updateFromUrl(); },
    serveis: {
      handler: function () {
        this.calculaPreuTotal();
        this.updateUrl();
        },
      deep: true
    },
    nomClient: function () { this.calculaPreuTotal(); },
    nomPressu: function () { this.calculaPreuTotal(); },
    /*
      preuTotal : function() {
    this.calculaPreuTotal();
    console.log("preuTotal: watch preuTotal: "+ this.preuTotal);
    //this.urlQuery = this.$route.query;
    //console.log(this.urlQuery);
      },
      totalServeisWeb: function() {
    this.calculaPreuTotal();
    //console.log("totalServeisWeb: watch preuTotal: "+ this.preuTotal);
      },
      $route: function() {
    this.urlQuery = this.$route.query;
    console.log("urlQuery is:");
    console.log(this.urlQuery);
      }
    */
  },
  mounted() {
    //console.log('dom Home mounted!')
    //this.updateFromUrl()
    //this.calculaPreuTotal()
    //this.updateFromUrl();

    //this.calculaPreuTotal()
    //this.updateUrl();
  },
  updated() {
    //console.log('dom Home updated!')
    //this.calculaPreuTotal();
    // this.updateFromUrl();
  },
  methods: {
    updateCurrentPresu() {
      let dataAvui = this.getCurrentDateTime();
      this.idPressu = this.getUniqueId();
      this.currentPressu = [];
      //this.calculaPreuTotal();
this.currentPressu.push({
id:this.idPressu, nomPressu:this.nomPressu, nomClient:this.nomClient, date:dataAvui, totalServeis:this.totalServeis,totalServeisWeb:this.totalServeisWeb, preuTotal:this.preuTotal, });
      this.serveis.map((servei) => { servei.selected ? this.currentPressu.push(servei) : 0 });
      //console.log(...this.currentPressu);

    },
    calculaPreuTotal() {
      this.preuTotal = 0;
      this.serveisPicked = [];
      this.serveisPicked = this.serveis.filter((item) => item.selected == true);
      // console.log(this.serveisPicked);
      this.totalServeis = this.serveisPicked.reduce(
        (accumulator, currentItem) => { return accumulator + currentItem.preu; }, 0);
      //console.log("Total serveis: "+totalServeis);
      this.calculaServeisWeb();
      this.showServeisweb == true ? (this.preuTotal = this.totalServeis + this.totalServeisWeb) : (this.preuTotal = this.totalServeis);
      this.preuTotal = this.totalServeis + this.totalServeisWeb;
      this.updateCurrentPresu();
      //console.log(this.preuTotal);
      return this.preuTotal;
    },
    calculaServeisWeb() {
      if ( this.showServeisweb) {
        this.totalServeisWeb = this.serveis[0].langs * this.serveis[0].pags * 30
      } else {
        this.totalServeisWeb = 0; this.serveis[0].langs = 0; this.serveis[0].pags = 0;
      }
      //return this.totalServeisWeb;
    },
    check(e, idx) {
      this.serveis[idx].selected = e.target.checked;
      console.log("↓ chek/unchek ↓ ");
      //console.log(this.serveis[idx]);
      this.serveis[idx] === 0 ? this.showServeisweb = true : this.showServeisweb = false;
      this.showServeisweb = this.serveis[0].selected;
      //console.log(this.showServeisweb);
      //console.log(selected, e.target.value );
      this.calculaPreuTotal();
    },
    addPressu() {
      if (this.nomPressu === "" || this.nomClient === "" || this.preuTotal === 0) {
        this.alert1 = true;
      } else {
        // la copia con JSON
        // https://www.kuworking.com/javascript-como-copiar-arrays
        // const myJSONCopy = JSON.parse(JSON.stringify(this.currentPressu))
        const pressupost = JSON.parse(JSON.stringify(this.currentPressu))
        //const pressupost = [];
        this.pressusList.push({ pressupost });
        console.log(this.pressusList);
        this.pressusListLength = this.pressusList.length;
        //this.sortBy = null;
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

updateFromUrl() {
this.urlQuery = this.$route.query;
this.serveis[0].selected = this.$route.query.web;
this.$route.query.web === "true" ? this.showServeisweb = true : this.showServeisweb = false;
this.serveis[0].langs = this.$route.query.langs;
this.serveis[0].pags = this.$route.query.pags;
this.serveis[1].selected = this.$route.query.seo;
this.serveis[2].selected = this.$route.query.ads;
//this.calculaServeisWeb();
//this.calculaPreuTotal();
//this.updateCurrentPresu()
//this.calculaPreuTotal();
//this.updateCurrentPresu()
//this.preuTotal = this.$route.query.total;
    },
    updateUrl() {
      // creating the parametric url
      //this.calculaPreuTotal();
      //this.updateCurrentPresu();
      this.$router.push({
        path: '/home', query: {
          // hash: this.idPressu,
          web:    this.serveis[0].selected,
          langs:  this.serveis[0].langs,
          pags:   this.serveis[0].pags,
          seo:    this.serveis[1].selected,
          ads:    this.serveis[2].selected,

          total:  this.preuTotal,
        }
      })

      this.urlQuery = this.$route.query;

    }
  },
  // end methods:


};
</script>

<template>
  <div id="v-home" class="maxW1300">
    <div id="ruta">{{ }}</div>

    <div id="c-formulari" class="flex one three-800 center">
      <MostraPressu :currentPressu="currentPressu" :preuTotal="preuTotal" />

      <form id="c-form" class="flex one center c-modul">
        <h2>Calculadora de Pressupostos</h2>
        <div id="f-camps">
          <div class="f-group">
            <input type="text" v-model="nomClient" placeholder="Nom client" />
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

      <LlistaPressus :pressusList="pressusList" :pressusListLength="pressusListLength" />
    </div>
  </div>
</template>


<style scoped>
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
