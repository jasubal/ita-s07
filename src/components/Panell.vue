<template>
<div id="c-panell">

<ul>
<li>Idiomes:
<button @click="subtract(serveisweb[0])">-</button>
<input type="number" v-model.number="serveisweb[0].num">
<button @click="add(serveisweb[0])">+</button>
<Modal :lab1="modals[0].lab1" :lab2="modals[0].lab2" :msg="modals[0].msg" ></Modal>
</li>

<li>Pàgines:
<button @click="subtract(serveisweb[1])">-</button>
<input type="number" v-model.number="serveisweb[1].num">
<button @click="add(serveisweb[1])">+</button>
<Modal :lab1="modals[1].lab1" :lab2="modals[1].lab2" :msg="modals[1].msg" ></Modal>
</li>
</ul>
idiomes: {{ serveisweb[0].num }} - pagines: {{ serveisweb[1].num }}
</div>
</template>

<script>
import Modal from "./Modal.vue";
export default {
    components: { Modal },
    props: ["serveisweb"],
    name: "Panell",
    beforeMount() {
        // this.serveisweb = this.serveisweb // save props data to itself's data and deal with it
    },
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
            console.log(this.serveisweb);
        },
        subtract(item) {
            item.num < 2 ? item.num = 1 : item.num--;
            this.$emit("serveisweb", this.serveisweb);
            console.log(this.serveisweb);
        },
    },
    components: { Modal }
}
</script>

<style>
#c-panell {
    padding: 1em;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    border: 2px solid #e8e5e5;
    border-radius: 10px;
}
li {
    margin: 0 0 .3em;
    display: flex;
    align-items: center;
    flex-wrap: nowrap;
    flex-direction: row;
}
input[type=number] {
    background: transparent;
    width: 3.1em;
    margin: 0 10px;
    text-align: center;
}
ul{
    display: flex;
    align-items: flex-end;
    flex-direction: column;
    text-align: left;
}
#c-modal .button {
    font-size: 1.2em;
    margin: 2px 10px 0;
    padding: 0 10px 0;
    border-radius: 50%;
    color: #fff;
    background: #25c781;
    cursor: pointer;
}

</style>
