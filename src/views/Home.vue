<template>
  <div id="v-home">
    <h1>Quins serveis necessites?</h1>

    <div id="c-formulari" class="flex one center">
      <form class="flex one center">


        <div id="choose-serveis" class="f-roup">
          <input
            id="check-pressu"
            type="checkbox"
            v-model="serveisPicked"
            value="500"
            @change="check($event)"
          />
          <label for="check-pressu" class="checkable">Pàgina web (500 €)</label>
          <div v-show="selected">
            <Panell :serveisweb="serveisweb" @serveisweb="serveisweb=$event" />
          </div>
          <input id="check-seo" type="checkbox" v-model="serveisPicked" value="300" />
          <label for="check-seo" class="checkable"> Consultoria SEO (300 €)</label>
          <input id="check-ads" type="checkbox" v-model="serveisPicked" value="400" />
          <label for="check-ads" class="checkable">Campanya de Publicitat (400 €)</label>
        </div>

   <div class="f-roup">
          <input type="text" v-model="nom" placeholder="Nom client" />
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
        { id:10, nom: "Pàgina web", preu: 500 },
        { id:20, nom: "Consultoria SEO", preu: 300 },
        { id:30, nom: "Campanya de Publicitat", preu: 400 },
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
      console.log(e.target.checked);
    },
    /*
        onChange(event) { let data = event.target.value; console.log(data); }
        */
  },
};
</script>

<style scoped>
#c-formulari { padding: 2em 0; }
form{
      max-width: 500px;
    background: #fff;
    padding: 1em;
    width: 100%;
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
</style>
