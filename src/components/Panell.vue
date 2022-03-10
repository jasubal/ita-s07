<template>
<div id="c-panell">

<ul>
<li><span>Idiomes:</span>

<button @click="subtract('langs')" >-</button>
<input v-model.number="serveis[0].langs">
<button @click="add('langs')">+</button>
<Modal :lab1="modals[0].lab1" :lab2="modals[0].lab2" :msg="modals[0].msg" ></Modal>
</li>

<li><span>Pàgines:</span>

<button @click="subtract('pags')">-</button>
<input v-model.number="serveis[0].pags">
<button @click="add('pags')">+</button>
<Modal :lab1="modals[1].lab1" :lab2="modals[1].lab2" :msg="modals[1].msg" ></Modal>
</li>
</ul>
<!-- idiomes: {{ serveis[0].pags}} - pagines: {{ serveis[0].langs }} -->
</div>
</template>

<script>
import Modal from "./Modal.vue";
export default {
    name: "Panell",
    components: { Modal },
    props: ["serveis"],
    data() {
        return {

modals: [
{lab1: "?",lab2:"Info",msg:"Aquest component ha de mostrar el número d'idiomes que tindrà la web"},
{lab1: "?",lab2:"Info",msg:"Aquest component ha de mostrar el número d'idiomes que tindrà la web"}
],

        };
    },
    methods: {
        add(item) {

            this.serveis[0][item]++;
            this.$emit("serveis", this.serveis);
            console.log(this.serveis[0]);
        },
        subtract(item) {
             this.serveis[0][item] <= 1 ?  this.serveis[0][item] = 1 :  this.serveis[0][item]--;
            this.$emit("serveis", this.serveis);
            console.log(this.serveis[0]);

        },
    },
}
</script>

<style scoped>
#c-panell { padding:0 1em; display: flex; flex-direction: column; align-items: flex-start; border: 2px solid #e8e5e5; border-radius: 10px; }
li { margin: 0 0 .3em; display: flex; align-items: center; flex-wrap: nowrap; flex-direction: row; }
li span { margin: 0 8px 0 0 }
input { background: transparent; width: 3.2em; margin: 0 10px; text-align: center; }
ul{ display: flex; align-items: flex-end; flex-direction: column; text-align: left; }

</style>
