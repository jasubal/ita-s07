
<script>
import { markRaw } from "vue";
import Panell from "../components/Panell.vue";
import Alert from "../components/Alert.vue";
import MostraPressu from "../components/MostraPressu.vue";
import LlistaPressus from "../components/LlistaPressus.vue";


export default {
  name: "Home",
  components: { Panell, Alert, MostraPressu, LlistaPressus },
  data() {
    return {

      nomClient: "",
      nomPressu: "",
      serveis: [
        { servei: "Pàgina web", preu: 500, selected: false, langs: 0, pags: 0,  },
        { servei: "Consultoria SEO", preu: 300, selected: false },
        { servei: "Campanya de Publicitat", preu: 400, selected: false },
      ],
      serveisweb: [
        { nom: "idioma", num: 1 }, { nom: "pages", num: 1 },
      ],
      serveisPicked: [],
      currentPressu: [],
      pressusList: [],
      pressusListLength: 0,
      preuTotal: 0,
      showServeisweb: false,
      alert1: false,
      labAlert1: "Alerta",
      msgAlert1: "Emplena nom del client,<br> nom del pressupost<br> i un servei com a mínim",

    };
  },
   mounted() {
    // this.nomPressu.length < 1 ? this.nomPressu = "nom pressupost "+this.getUniqueId() : 0
  },
  watch : {
    preuTotal:function() {
      console.log("watch this preuTotal: "+ this.preuTotal);
      }

  },
  methods: {

    updateCurrentPresu() {
      this.currentPressu = [];
      let dataAvui = this.getCurrentDateTime();
      this.currentPressu.push( {
        id: this.getUniqueId(),
        nomPressu:this.nomPressu,
        nomClient:this.nomClient,
        date: dataAvui,
        preuTotal:this.preuTotal,

        } );

   this.serveis.map((servei) => {servei.selected ? this.currentPressu.push(servei) : 0});
    //console.log(this.currentPressu);
    },

    calcularPreuTotal() {
      this.preuTotal = 0;
      const totalServeis = this.serveisPicked.reduce((partialSum, num) => partialSum + parseInt(num), 0 );
      const totalServeisWeb = this.serveisweb[0].num * this.serveisweb[1].num * 30;
      this.serveis[0].langs = this.serveisweb[0].num;
      this.serveis[0].pags = this.serveisweb[1].num;
      this.showServeisweb == true ? (this.preuTotal = totalServeis + totalServeisWeb) : (this.preuTotal = totalServeis);
      this.updateCurrentPresu();
      return this.preuTotal;
    },

    check(e,idx) {
      this.serveis[idx].selected = e.target.checked;
      console.log("↓ chek/unchek ↓ ");
      //console.log(this.serveis[idx]);
      this.serveis[idx] === 0 ? this.showServeisweb = true : this.showServeisweb = false;
      this.showServeisweb = this.serveis[0].selected;
      //console.log(this.showServeisweb);
      //console.log(selected, e.target.value );
      this.calcularPreuTotal();
    },
    addPressu(){
      if ( this.nomPressu === "" || this.nomClient === "" || this.preuTotal === 0 ) {
          this.alert1 = true;
      }else{
    // la copia con JSON
    // https://www.kuworking.com/javascript-como-copiar-arrays
    // const myJSONCopy = JSON.parse(JSON.stringify(this.currentPressu))
    const pressupost = JSON.parse(JSON.stringify(this.currentPressu))
    //const pressupost = [];
      this.pressusList.push( { pressupost } );
      this.pressusListLength = this.pressusList.length;
      //this.sortBy = null;
        }
      },
    getUniqueId() {
      //return new Date().getTime();
      let uniqueId = window.crypto.getRandomValues(new Uint32Array(1))[0];
      return uniqueId.toString(16);
    },
    getCurrentDateTime(){
    let today = new Date();
    let date = today.getFullYear()+'-'+(today.getMonth()+1)+'-'+today.getDate();
    let time = today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
    return date+' '+time;
    }

  },


};
</script>

<template>
  <div id="v-home" class="maxW1300">

    <div id="c-formulari" class="flex one three-800 center">

<MostraPressu :currentPressu="currentPressu" :preuTotal="preuTotal" />

      <form id="c-form" class="flex one center c-modul" >
        <h2>Calculadora de Pressupostos</h2>
        <div id="f-camps">
        <div class="f-group">
          <input type="text" v-model.lazy="nomClient" placeholder="Nom client" />
              </div>
             <div class="f-group">
            <input type="text" v-model.lazy="nomPressu" placeholder="Nom Pressupost" />
          </div>
        <div id="choose-serveis" class="f-group">
          <input id="check-pressu" type="checkbox" v-model="serveisPicked" value="500" @change="check($event, 0)" />
          <label for="check-pressu" class="checkable">Pàgina web (500€)</label>
          <div v-if="showServeisweb">
            <Panell :serveisweb="serveisweb" @serveisweb="serveisweb = $event" />
          </div>

          <input id="check-seo" type="checkbox" v-model="serveisPicked" value="300" @change="check($event, 1)" />
          <label for="check-seo" class="checkable">
            Consultoria SEO (300 €)</label>

          <input id="check-ads" type="checkbox" v-model="serveisPicked" value="400" @change="check($event, 2)" />
          <label for="check-ads" class="checkable"
            >Campanya de Publicitat (400 €)</label>
        </div>

        <h3>Preu total: {{ calcularPreuTotal() }} €</h3>
          <div class="f-group">
            <div v-if="alert1">
            <Alert :lab1="labAlert1" :msg="msgAlert1" @alert="alert1 = $event"  ></Alert>
            </div>
            <button @click="addPressu()" >Guarda el Pressupost</button>
          </div>


</div>
      </form>

<LlistaPressus :pressusList="pressusList" :pressusListLength="pressusListLength" />

    </div>
  </div>
</template>


<style scoped>
#v-home { padding: 0 }
#c-formulari { padding: 0; }
h3 { margin: 0; padding: 0; }
form {
  display: flex;
    align-content: flex-start;
}

input,
textarea { max-width: 18em; margin: 10px 0 0; }
input[type="checkbox"] { width: 1em; }
#choose-serveis { width: 100%; display: flex; flex-direction: column; flex-wrap: wrap; align-content: center; align-items: flex-start; }
label { margin: 10px 0; cursor: pointer; }


@media (min-width: 56.25em) {
form {
    background: #fdfdfd;
    width: 33%;
  }
}

@media (min-width: 75em) {

 }

</style>
