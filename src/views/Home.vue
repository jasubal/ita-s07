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
      preuTotal: 0,
      elspressus: [],
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
  methods: {
    updateCurrentPresu() {
      this.currentPressu = [];
      this.currentPressu.push( {resum: { preu:this.preuTotal, nomClient:this.nomClient, nomPressu:this.nomPressu } } );
      this.currentPressu.push( {productes: [] } );
      this.serveis.forEach((servei) => {
        (servei.selected) ? this.currentPressu[1].productes.push(servei) : 0; //si el servei està seleccionat, l'afegim al array de productes
      });
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
    addPressu(e) {
      e.preventDefault();
if ( this.nomClient === "" || this.preuTotal === 0 ) {
        this.alert1 = true;
} else {
      this.elspressus.push({pressupost:[]});
      //this.elspressus[this.elspressus.length-1].pressupost.push( {this.currentPressu}  );
      console.log("added Pressu");
}
    }
  },

};
</script>

<template>
  <div id="v-home">

    <div id="c-formulari" class="c-modul flex one three-800 center">

<MostraPressu :currentPressu="currentPressu" :preuTotal="preuTotal" />

      <form class="flex one center" >
        <h2>Calculadora de pressupostos</h2>
        <div id="choose-serveis" class="f-roup">
          <input
            id="check-pressu"
            type="checkbox"
            v-model="serveisPicked"
            value="500"
            @change="check($event, 0)"
          />
          <label for="check-pressu" class="checkable">Pàgina web (500 €)</label>
          <div v-if="showServeisweb">
            <Panell
              :serveisweb="serveisweb"
              @serveisweb="serveisweb = $event"
            />
          </div>

          <input
            id="check-seo"
            type="checkbox"
            v-model="serveisPicked"
            value="300"
            @change="check($event, 1)"
          />
          <label for="check-seo" class="checkable">
            Consultoria SEO (300 €)</label
          >

          <input
            id="check-ads"
            type="checkbox"
            v-model="serveisPicked"
            value="400"
            @change="check($event, 2)"
          />
          <label for="check-ads" class="checkable"
            >Campanya de Publicitat (400 €)</label
          >
        </div>

        <div class="f-roup">
          <input type="text" v-model="nomClient" placeholder="Nom client" />
          <input type="text" v-model="nomPressu" placeholder="Nom Pressupost" />
        </div>

        <div id="form-outputs">

          <div class="f-group">Preu total: {{ calcularPreuTotal() }} €</div>
          <div class="f-group">
            <div v-if="alert1">
            <Alert :lab1="labAlert1" :msg="msgAlert1" @alert="alert1 = $event"  ></Alert>
            </div>
            <button type="submit" @click="addPressu($event)">Guarda el Pressupost</button></div>
        </div>
      </form>

<LlistaPressus :elspressus="elspressus" />

    </div>
  </div>
</template>


<style scoped>
#v-home { padding: 10px 10px; }
#c-formulari { padding: 0; }
h3 { margin: 0; padding: 0; }
form { max-width: 430px; background: #fdfdfd; padding: 0; width: 100%; }
.f-group { margin: 1em 0 0; }
input,
textarea { max-width: 18em; margin: 10px 0 0; }
input[type="checkbox"] { width: 1em; }
#choose-serveis { width: 100%; display: flex; flex-direction: column; flex-wrap: wrap; align-content: center; align-items: flex-start; }
label { margin: 10px 0; cursor: pointer; }
</style>
