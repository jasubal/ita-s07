<template>
<div id="c-llistaPressus" class="c-modul">

<div v-if="pressusList.length > 0 " id="llistat">
<h2>Pressupost list</h2>
<p>Pressuposts guardats: {{pressusList.length}}</p>
<ul>
    <li class="pressItem" v-for="(item,index ) in pressusList" :key='index' >
Nom pressupost: {{ item.pressupost[0].nomPressu  }} <br>
Nom client:     {{ item.pressupost[0].nomClient  }} <br>
Data:           {{ item.pressupost[0].dataPressu }} <br>
Preu total:     {{ item.pressupost[0].preuTotal  }} <br>
Serveis:
<div v-for="(s,index) in item.pressupost" :key='index'>
    <span v-if="s.servei">{{s.servei}}</span>
</div>

<hr>
     </li>
  </ul>

<!--
 Nom Presupost: {{ pressupost[0].nomPressu }}
        {{ pressupost.resum.nomPressu }}

 -->

</div>
    <pre>{{ pressusList }}</pre>
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
renderPressu(idx) {
    let output = '';
    let resum = this.pressusList[idx].resum;
    let productes = this.pressusList[idx].productes;
    output += '<h3 class="tit">Resum</h3>';
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
    background: rgb(245, 245, 245);
    border: 1px solid #CCC;
    min-height: 6em;
    width: 90%;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    padding: 10px;
}
@media (min-width: 56.25em) {

}

@media (min-width: 75em) {

 }
</style>
