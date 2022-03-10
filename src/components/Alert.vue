<template>
<div id="c-alert">
<div id="alert" @click="closeAlert()">
<div id="alertpanel">
 <div id="x"> <span class="x">X</span> </div>
<h2 v-html="lab1"></h2>
<p v-html="msg"></p>
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
    align-content: center;
    align-items: center;
background: #ffffff6b;
    display: flex;
    flex-direction: column;
    height: 100vh;
    justify-content: center;
    left: 0;
    position: fixed;
    top: 0;
    width: 100vw;
}
#alert {
    background: #ffffff;
    border-radius: 20px;
    box-shadow: 1px 1px 13px 1px #e9e8e8;
    cursor: pointer;
    height: auto;
    line-height: 1.4;
    max-width: 540px;
    padding: 1em 2em;
    width: 100%;
}

#alertpanel { font-size: 1.2em; position: relative; }
#alertpanel h2 {
    color: #e70000;
    font-size: 1.4em;
    letter-spacing: 1px;
    border-top: none;
}
#x {
    position: absolute;
    right: 0;
    z-index: 99999;
}
span.x {
    background: #eee;
    border-radius: 100%;
    color: #e70000;
    font-size: 1em;
    height: 34px;
    padding: 2px 0 0;
    position: absolute;
    right: 0;
    width: 32px;
}


@media (min-width: 75em) {
#c-alert {
    position: absolute;
    width: 100vw;
    height: 100vh;
    top: 0;
    left: 0;
    }
}


</style>
