<template>
<div id="c-llistaPressus" class="c-modul">

<div v-if="pressusList.length > 0 " id="llistat">
<h2>Listat de Pressupostos <span>({{pressusList.length}})</span></h2>
<div class="c-group">
<input id="searchInput" @keyup="handleInput()" type="text" placeholder="Cerca pressupostos..." v-model="searchInput" />
<button id="lupa" @click="handleInput()">🔎</button>
</div>
<div class="c-group">
    <button @click="sortBy='nomPressuAZ'">A-Z</button>
    <button @click="sortBy='nomPressuZA'">Z-A</button>
    <button @click="sortBy='preuTotalMenor'">Preu↑</button>
    <button @click="sortBy='preuTotalMajor'">Preu↓</button>
    <button @click="sortBy='date'">Data</button>
    <button @click="sortBy=null">RESET</button>
</div>
<ul id="list-items">
    <li class="pressItem" v-for="(item,index ) in changeList()" :key='index' >
        <div v-html="renderPressu(item)"></div>
     </li>
  </ul>

<!--
    <p>{{searchInput}}</p>
     <pre>{{pressusList2sort}}</pre>
      <pre>{{ pressusList }}</pre>
 -->

</div>

</div>
</template>

<script>
export default {

    name: "LlistaPressus",
    props: ["pressusList","pressusListLength"],
    data() {
        return {
            sortBy: null,
            searchInput: "",
            pressusList2sort: [],
            pressusListReversed: [],
            pressusListResults: [],

        }
    },
    updated() {
        //console.log('dom LlistaPressus updated!')
     },
    mounted() {
        //console.log('dom LlistaPressus mounted!')
     },

watch: {

    pressusListLength: function(){
        this.sortBy=null;
        this.changeList();
        // console.log("pressusListLength watch sortBy="+this.sortBy);
        // this.sortList();
    },
    sortBy: function(){
        this.sortList();
        console.log("watch sortBy="+this.sortBy);
    },

},
onBeforeUpdate: function(){
    console.log("onBeforeUpdate");
},

methods: {

renderPressu(item) {
    let output = '';
    let resum = item.pressupost[0]
    output += "<strong>Nom presupost: "+resum.nomPressu+ "</strong><br>";
    output += "Client: "+resum.nomClient+"<br>";
    output += "Data: "+resum.date+" / ";
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
},

changeList(){
    if(this.sortBy === null) { return  this.pressusListReversed = this.pressusList.slice().reverse(); }
    else{ return this.pressusList2sort }
},
sortList(){
    this.pressusList2sort = this.pressusList;


if (this.sortBy === 'nomPressuAZ') {
    this.pressusList2sort.sort((a,b)=>(
        a.pressupost[0].nomPressu.toLowerCase() > b.pressupost[0].nomPressu.toLowerCase() ? 1 : -1
    ));
    console.log('sort by nomPressuAZ');
    /*
    this.pressusList2sort.sort(function(a,b) {
        if (a.pressupost[0].nomPressu < b.pressupost[0].nomPressu) { return -1; }
        if (a.pressupost[0].nomPressu > b.pressupost[0].nomPressu) { return  1; }
    });
    */
} else if ((this.sortBy === 'nomPressuZA') ){
    this.pressusList2sort.sort((a,b)=>(
        a.pressupost[0].nomPressu.toLowerCase() > b.pressupost[0].nomPressu.toLowerCase() ? -1 : 1
    ));
    console.log('sort by nomPressuZA');

} else if (this.sortBy === 'preuTotalMajor') {
    this.pressusList2sort.sort((a,b)=>(
        a.pressupost[0].preuTotal > b.pressupost[0].preuTotal ? -1 : 1
    ));
    console.log('sort by preuTotalMajor');

} else if (this.sortBy === 'preuTotalMenor') {
    this.pressusList2sort.sort((a,b)=>(
        a.pressupost[0].preuTotal > b.pressupost[0].preuTotal ? 1 : -1
    ));
    console.log('sort by preuTotalMenor');

} else if (this.sortBy === 'date') {
    this.pressusList2sort.sort((a,b)=>(
        a.pressupost[0].date > b.pressupost[0].date ? 1 : -1
    ));
    console.log('sorted by date');

} else if (this.sortBy === 'searchTerm') {
      console.log('sort by searchTerm');
      if (this.searchInput !== '') {
  this.pressusListResults = this.pressusList2sort.filter((a) => (
    a.pressupost[0].nomPressu.toLowerCase().includes(this.searchInput.toLowerCase())
  ));
    this.pressusList2sort = this.pressusListResults;
      console.log(this.pressusList2sort);
      } else {
        console.log('no searchTerm');
        this.sortBy === null;
        this.changeList();
      }
}
else {
    console.log('back to original list');
      this.changeList();
}


},
handleInput() {
      console.log(this.searchInput);
      this.sortBy="searchTerm";
      //this.changeList();
      this.sortList();
    },

} }
</script>

<style>
h2 span { font-size: 0.6em; }
.c-group {
    display: flex;
    justify-content: center;
    margin: 12px;
    align-items: center;
}
.c-group  input { border: 1px solid #e0e0e0; max-width: 80%; }
.c-group  button { font-size: .8em; margin: 2px; }
#searchInput{
    border: 1px solid #e0e0e0;
    max-width: 75%;
    margin: 0 10px;
}
#lupa {
    height: 100%;
    margin: 0;
    padding: 4px 9px;
    border: 1px solid;
    font-size: 1em;
    background: #f9f9f900;
}
#llistat ul {
    flex-wrap: wrap;
    align-items: center;
    flex-direction: column;
    padding-inline-start: 24px;
    overflow-y: scroll;
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
#llistat ul {
    flex-wrap: wrap;
    align-items: center;
    flex-direction: column;
    padding-inline-start: 24px;
    overflow-y: scroll;
    max-height: 50vh;
}
 }
</style>
