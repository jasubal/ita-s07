<template>
<div id="c-llistaPressus" class="c-modul">

<div v-if="pressusList.length > 0 " id="llistat">
<h2>Listat de Pressupostos</h2>
<p>Pressupostos guardats: {{pressusList.length}}</p>
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

        }
    },
    methods: {

    renderPressu(item) {
    let output = '';
    let resum = item.pressupost[0]
/* */
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


}
</script>

<style>
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
