<template>
  <div id="v-home">
    <h1>Quins serveis necessites?</h1>

    <div id="c-formulari" class="flex one two-800 center">

      <form class="flex one center">

<div id="choose-serveis" class="f-roup">

<input id="check-pressu" type="checkbox" v-model="serveisPicked" value="500" @change="check($event)" />
<label for="check-pressu" class="checkable">Pàgina web (500 €)</label>

<div v-show="selected">
            <Panell :serveisweb="serveisweb" @serveisweb="serveisweb=$event" />
</div>

<input id="check-seo" type="checkbox" v-model="serveisPicked" value="300"  />
<label for="check-seo" class="checkable"> Consultoria SEO (300 €)</label>

<input id="check-ads" type="checkbox" v-model="serveisPicked" value="400" />
<label for="check-ads" class="checkable">Campanya de Publicitat (400 €)</label>

</div>

  <div class="f-roup">
    <input type="text" v-model="nomClient" placeholder="Nom client" />
    <input type="text" v-model="nomPressu" placeholder="Nom Pressupost" />
  </div>

  <div id="form-outputs">

    <div v-if="nomPressu != ''">
          {{ nomPressu }}
        </div>
        <div v-if="nomClient != ''">
          Pressupost per a: {{ nomClient }}
        </div>

        <div class="f-group">Preu total: {{ calcularPreuTotal() }} €</div>
         <div class="f-group"><button>Guarda el Pressupost</button></div>
      </div>



      </form>

    </div>
  </div>
</template>


<script>
import Panell from "../components/Panell.vue";
export default {
  name: "Home",
  components: { Panell },
  data() {
    return {
      nomClient: "", nomPressu: "",
      serveis: [
        { id:10, nom: "Pàgina web", preu: 500, selected: false },
        { id:20, nom: "Consultoria SEO", preu: 300, selected: false },
        { id:30, nom: "Campanya de Publicitat", preu: 400, selected: false },
      ],
      serveisweb: [
        { id:11, nom: "idioma", num: 1 },
        { id:12, nom: "pages", num: 1 },
    ],
      serveisPicked: [],
      selected: false,
      preuTotal: 0,
    };
  },
  methods: {
    calcularPreuTotal() {
      const totalServeis = this.serveisPicked.reduce(
        (partialSum, num) => partialSum + parseInt(num), 0
      );
      const totalServeisWeb = (this.serveisweb[0].num * this.serveisweb[1].num * 30);
      return totalServeis + totalServeisWeb
    },
    check(e) {
      this.selected = e.target.checked;
      console.log(this.selected, e.target.value );
    },
    /*
        onChange(event) { let data = event.target.value; console.log(data); }
        */
  },
};
</script>

<style scoped>
#c-formulari { padding: 0; }
form{ max-width: 500px; background: #fff; padding: 1em; width: 100%; }
.f-group { margin: 1em 0 0; }
input, textarea { max-width: 18em; margin: 10px 0 0; }
input[type="checkbox"] { width: 1em; }
#choose-serveis { width: 100%; display: flex; flex-direction: column; flex-wrap: wrap; align-content: center; align-items: flex-start; }
label { margin: 10px 0; cursor: pointer; }
</style>
