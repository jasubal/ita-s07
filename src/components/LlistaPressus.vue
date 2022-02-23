<template>
<div id="c-llistaPressus" class="c-modul">

<div v-if="pressusList.length > 0 " id="llistat">
<h2>Listat de Pressupostos <span>({{pressusList.length}})</span></h2>
<div class="c-group">
<input type="search" v-model.lazy="search" placeholder="Cerca" />
</div>
<div class="c-group">
    <button @click="sortBy='nomPressu'">Ordena A-Z</button>
    <button @click="sortBy='preuTotal'">Ordena Preu</button>
    <button @click="sortList()">test</button>
</div>
 <pre>{{pressusList2sort}}</pre>
<ul>
    <li class="pressItem" v-for="(item,index ) in pressusList" :key='index' >
        <div v-html="renderPressu(item)"></div>
     </li>
  </ul>

<!--
      <pre>{{ pressusList }}</pre>
 -->

</div>

</div>
</template>

<script>
export default {

    name: "LlistaPressus",
    props: ["pressusList"],
    data() {
        return {
            sortBy: null,
            pressusList2sort: [],
        }
    },
    watch: {
        sortBy: function(){
            this.sortList() },
    },
    methods: {
sortList(){
this.pressusList2sort = this.pressusList.slice();
if (this.sortBy === 'nomPressu') {
    console.log('sort by nomPressu');
this.pressusList2sort.sort(function(a,b) {
        if (a.pressupost[0].nomPressu < b.pressupost[0].nomPressu) { return -1; }
        if (a.pressupost[0].nomPressu > b.pressupost[0].nomPressu) { return 1; }
        return 0;
    });
} else if (this.sortBy === 'preuTotal') {
    console.log('sort by preuTotal');
this.pressusList2sort .sort(function(a,b) {
        if (a.pressupost[0].preuTotal < b.pressupost[0].preuTotal) { return -1; }
        if (a.pressupost[0].preuTotal > b.pressupost[0].preuTotal) { return 1; }
        return 0;
    });
} else {
    console.log('sort by null');
    // reset sort
 this.pressusList2sort.sort(function(a,b) { if (a.pressupost[0].id < b.pressupost[0].id) { return -1; }
        if (a.pressupost[0].id > b.pressupost[0].id) { return 1; }
        return 0;
    });
}
},

    renderPressu(item) {
    let output = '';
    let resum = item.pressupost[0]
    output += "<strong>Nom presupost: "+resum.nomPressu+ "</strong><br>";
    output += "Client: "+resum.nomClient+"<br>";
    output += "Data: "+resum.dataPressu+" / ";
    output += "ID: "+resum.id+"<br>";
    output += "<strong>Inclou: </strong> ";
        for(let i=1; i<item.pressupost.length; i++) {
        if (item.pressupost[i].langs > 0) {
        let totalServeisWeb = item.pressupost[i].langs * item.pressupost[i].pags * 30;
    output += item.pressupost[i].servei + ": "+item.pressupost[i].preu+"€<br>";
    output += item.pressupost[i].langs + " idioma/es + "+item.pressupost[i].pags+" pàgina/es : "+totalServeisWeb+"€<br>";
        } else {
    output += item.pressupost[i].servei + ": "+item.pressupost[i].preu+"€<br>";
        }
    }
    output += "<strong>Preu total: "+resum.preuTotal+"€</strong><br>";
    return output;
}

},
// computed: {

// }
}
</script>

<style>
h2 span { font-size: 0.6em; }
.c-group {
    display: flex;
    justify-content: center;
    margin: 12px;
}
.c-group  input { border: 1px solid #e0e0e0; max-width: 80%; }
.c-group  button { font-size: .8em; margin: 2px; }
#llistat ul {
    flex-wrap: wrap;
    align-items: center;
    flex-direction: column;
}
li.pressItem {
    align-items: flex-start;
    background: rgb(249 249 249);
    border-radius: 10px;
    border: 1px solid #59affa;
    box-shadow: 1px 1px 9px #e3e3e3c9;
    display: flex;
    flex-direction: column;
    padding: 1em;
    text-align: left;
    width: 96%;
}
@media (min-width: 56.25em) {

}

@media (min-width: 75em) {

 }
</style>
