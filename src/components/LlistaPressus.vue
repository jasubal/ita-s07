<template>
<div id="c-llistaPressus" class="c-modul">

<div v-if="pressusList.length > 0 " id="llistat">
<h2>Pressupost list</h2>
<!-- <pre>{{llistaPressus}}</pre> -->
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
    }



}
</script>

<style>
#llistat {
    display: flex;
}
</style>
