<template>
<div id="c-llistaPressus" class="c-modul">

<div v-if="pressusList.length > 0 " id="llistat">
<h2>Pressupost list</h2>

<ul>
    <li class="pressItem" v-for="(item,index) in pressusList" :key="item.id">
    Pressupost index: {{ index }} <br>
    {{ item }}



        </li>
  </ul>

<pre> {{ pressusList }}</pre>
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

#llistat h2 {
    position: sticky;
    right: 0;
    z-index: 9999999999;
    top: 0;
    background: #FFF;
}
.pressItem {
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
