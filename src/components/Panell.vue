<template>
<div id="c-panell">

<ul>
<li><span>Idiomes:</span>
<button @click="subtract(serveisweb[0])">-</button>
<input v-model.number="serveisweb[0].num">
<button @click="add(serveisweb[0])">+</button>
<Modal :lab1="modals[0].lab1" :lab2="modals[0].lab2" :msg="modals[0].msg" ></Modal>
</li>

<li><span>Pàgines:</span>
<button @click="subtract(serveisweb[1])">-</button>
<input v-model.number="serveisweb[1].num">
<button @click="add(serveisweb[1])">+</button>
<Modal :lab1="modals[1].lab1" :lab2="modals[1].lab2" :msg="modals[1].msg" ></Modal>
</li>
</ul>
<!--idiomes: {{ serveisweb[0].num }} - pagines: {{ serveisweb[1].num }}-->
</div>
</template>

<script>
import Modal from "./Modal.vue";
export default {
    name: "Panell",
    components: { Modal },
    props: ["serveisweb"],
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
            item.num++;
            this.$emit("serveisweb", this.serveisweb);
            //console.log(this.serveisweb);
        },
        subtract(item) {
            item.num < 1 ? item.num = 1 : item.num--;
            this.$emit("serveisweb", this.serveisweb);
            //console.log(this.serveisweb);
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
