<template>
  <div id="c-home">
    <h1>Què vols fer?</h1>

    <div id="c-formulari" class="flex one center">
      <form class="flex one center">
        <div class="f-roup">
          <input type="text" v-model="nom" placeholder="Nom client" />
        </div>

        <div id="choose-serveis" class="f-roup">
          <input
            id="ch-pressu"
            type="checkbox"
            v-model="picked"
            value="500"
            @change="check($event)"
          />
          <label for="ch-pressu" class="checkable">Pàgina web (500 €)</label>
          <div v-show="selected">
            <Panell :webfeatures="webfeatures" @webfeatures="webfeatures=$event" />
          </div>
          <input id="ch-seo" type="checkbox" v-model="picked" value="300" />
          <label for="ch-seo" class="checkable"> Consultoria SEO (300 €)</label>
          <input id="ch-ads" type="checkbox" v-model="picked" value="400" />
          <label for="ch-ads" class="checkable">Campanya de Publicitat (400 €)</label>
        </div>
      </form>
      <div id="form-outputs">
        <div v-if="nom != ''">
          <p>Pressupost per a: {{ nom }}</p>
        </div>

        <div class="f-roup">Preu total: {{ calcularPreuTotal() }} €</div>
      </div>
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
      nom: "",
      serveis: [
        { id: "ch-pressu", nom: "Pàgina web", preu: 500 },
        { id: "ch-seo", nom: "Consultoria SEO", preu: 300 },
        { id: "ch-ads", nom: "Campanya de Publicitat", preu: 400 },
      ],
      webfeatures: [
        { nom: "idioma", num: 1 },
        { nom: "pages", num: 1 },
    ],
      picked: [],
      selected: false,
      preuTotal: 0,
    };
  },
  methods: {
    calcularPreuTotal() {
      const totalPicked = this.picked.reduce(
        (partialSum, num) => partialSum + parseInt(num),
        0
      );
      return totalPicked;
    },
    check(e) {
      this.selected = e.target.checked;
      console.log(e.target.checked);
    },
    /*
        onChange(event) { let data = event.target.value; console.log(data); }
        */
  },
};
</script>

<style>
#c-formulari {
  background: #ebebeb;
}
.f-roup {
  margin: 1em 0 0;
}
input,
textarea,
.select select {
  max-width: 18em;
}

input[type="checkbox"] {
  width: 1em;
}
#choose-serveis {
    width: 25em;
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
</style>
