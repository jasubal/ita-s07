
<template>
  <div id="v-home">

    <div id="c-formulari" class="flex one three-800 center">

<MostraPressu :currentPressu="currentPressu" :preuTotal="preuTotal" />

      <form class="flex one center c-modul" >
        <h2>Calculadora de pressupostos</h2>
        <div class="f-roup">
          <input type="text" v-model.lazy="nomClient" placeholder="Nom client" />
              </div>
        <div id="choose-serveis" class="f-roup">
          <input id="check-pressu" type="checkbox" v-model="serveisPicked" value="500" @change="check($event, 0)" />
          <label for="check-pressu" class="checkable">Pàgina web (500 €)</label>
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


          <div class="f-roup">
            <input type="text" v-model.lazy="nomPressu" placeholder="Nom Pressupost" />
          </div>
               <div class="f-roup">
            <div v-if="alert1">
            <Alert :lab1="labAlert1" :msg="msgAlert1" @alert="alert1 = $event"  ></Alert>
            </div>
            <button @click="addPressu()" >Guarda el Pressupost</button>
            </div>

      </form>

<LlistaPressus :pressusList="pressusList" />

    </div>
  </div>
</template>

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
      nomClient: "",
      nomPressu: "",
      serveis: [
        { nom: "Pàgina web", preu: 500, selected: false, langs: 0, pags: 0,  },
        { nom: "Consultoria SEO", preu: 300, selected: false },
        { nom: "Campanya de Publicitat", preu: 400, selected: false },
      ],
      serveisweb: [
        { nom: "idioma", num: 1 }, { nom: "pages", num: 1 },
      ],
      serveisPicked: [],
      showServeisweb: false,
      currentPressu: [],
      pressu2add: [],
      preuTotal: 0,
      pressusList: [],
      alert1: false,
      labAlert1: "Alerta",
      msgAlert1: "Emplena nom del client, i un servei com a mínim",
    };
  },
  watch : {
    preuTotal:function() {
      console.log("watch this preuTotal: "+ this.preuTotal);
      }

  },
    mounted() {
      // this.nomPressu.length < 1 ? this.nomPressu = "nom pressupost "+this.getUniqueId() : 0

  },
  methods: {
    updateCurrentPresu() {
      this.currentPressu = [];
      let dataAvui = new Date().toLocaleDateString()

      this.currentPressu.push( {resum: {
        id: this.getUniqueId(),
        dataPressu: dataAvui,
        preu:this.preuTotal,
        nomClient:this.nomClient,
        nomPressu:this.nomPressu
        } } );

      this.currentPressu.push( {productes:[] } );
      this.serveis.map((servei) => {servei.selected ? this.currentPressu[1].productes.push(servei) : 0});
      // console.log(this.currentPressu);
    },
    calcularPreuTotal() {
      this.preuTotal = 0;
      const totalServeis = this.serveisPicked.reduce( (partialSum, num) => partialSum + parseInt(num),0 );
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
      console.log(this.serveis[idx]);
      this.serveis[idx] === 0 ? this.showServeisweb = true : this.showServeisweb = false;
      this.showServeisweb = this.serveis[0].selected;
      //console.log(this.showServeisweb);
      //console.log(selected, e.target.value );
      this.calcularPreuTotal();
    },
    addPressu(){
      if ( this.nomClient === "" || this.preuTotal === 0 ) {
          this.alert1 = true;
      }else{
      this.pressu2add = this.currentPressu.map( pressu => pressu);
      this.pressusList.push( { pressupost:[] } );
        // this.nomPressu.length > 0 ? this.nomPressu=this.nomPressu : this.nomPressu = "pressu"+this.getUniqueId() ;
        // this.pressusList.push( {pressupost:{ pressu2add }, });
        //this.currentPressu});
      //this.pressusList[this.pressusList.length-1].pressupost.push(this.currentPressu);
      this.pressusList[this.pressusList.length-1].pressupost.push(this.pressu2add);

        }
      },
    getUniqueId() {
      //return new Date().getTime();
      let uniqueId = window.crypto.getRandomValues(new Uint32Array(1))[0];
      return uniqueId.toString(16);
    },

  },


};
</script>


<style scoped>
#v-home { padding: 0 }
#c-formulari { padding: 0; }
h3 { margin: 0; padding: 0; }
.f-group { margin: 1em 0 0; }
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
