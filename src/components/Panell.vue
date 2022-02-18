<template>
<div id="c-panell">

<ul>
<li>
    Número d'idiomes:
<button @click="subtract(webfeatures[0])">-</button>
<input type="number" v-model.number="webfeatures[0].num">
<button @click="add(webfeatures[0])">+</button>
</li>
<li>
    Número de pàgines:
<button @click="subtract(webfeatures[1])">-</button>
<input type="number" v-model.number="webfeatures[1].num">
<button @click="add(webfeatures[1])">+</button>
</li>
idiomes: {{ webfeatures[0].num }} - pagines: {{ webfeatures[1].num }} -
</ul>
</div>
</template>

<script>

export default {
props: ['webfeatures'],
name: 'Panell',
beforeMount () {
  // this.webfeatures = this.webfeatures // save props data to itself's data and deal with it
},
data(){
    return {
    }

},
methods: {
add(item){
    item.num++;
    this.$emit('webfeatures', this.webfeatures);
        console.log(this.webfeatures);
},
subtract(item){
    item.num < 2 ? item.num = 1 : item.num--;
    this.$emit('webfeatures',this.webfeatures);
        console.log(this.webfeatures);
},

}
}
</script>

<style>
#c-panell {
    padding: 1em;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    border: 2px solid;
    border-radius: 10px;
}
input[type=number] {
    width: 3.6em;
    margin: 0 10px;
}
ul{
    display: flex;
    align-items: flex-end;
    flex-direction: column;
    text-align: left;
}
</style>
