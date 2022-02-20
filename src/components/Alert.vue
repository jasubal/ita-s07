<template>
<div id="c-alert">
<div id="alert" @click="closeAlert()">
<div id="panell">
    <div id="x">
    <span class="x">X</span>
    </div>
<h2>{{lab1}}</h2>
<hr>
{{ msg }}
</div>

</div>


</div>
</template>

<script>
export default {
    name: 'Alert',
    props: ['lab1', 'msg'],
    data() {
        return { }
    },
    methods: {
        closeAlert() {
            this.$emit('alert',false);
            console.log('alert closed');
        }
    }
}
</script>

<style>
#c-alert {
    position: absolute;
    width: 100vw;
    height: 100vh;
    top: 0;
    left: 0;
    background: #ffffffbd;
    display: flex;
    flex-direction: column;
    align-content: center;
    justify-content: center;
    align-items: center;
}
#alert {
    cursor: pointer;
    max-width: 600px;
    background: #ffffff;
    padding: 1em;
    width: 100%;
    height: 40vh;
    border-radius: 20px;
    box-shadow: 1px 1px 13px 1px #e9e8e8;
    max-height: 20em;
}
.close {
    position: absolute;
    font-size: 1.5em;
}
</style>
