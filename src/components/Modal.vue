<template>
<div id="c-modal">
<label for="modal_1" class="button">{{ lab1 }}</label>
  <div class="modal">
  <input id="modal_1" type="checkbox" />
  <label for="modal_1" class="overlay"></label>
  <div id="v-modal">
    <header>
      <h3>{{ lab2 }}</h3>
      <label for="modal_1" class="close">&times;</label>
    </header>
    <section class="content">
{{ msg }}
    </section>

  </div>
</div>
</div>
</template>

<script>
export default {
    name: 'Modal',
    props: ['lab1','lab2', 'msg'],
    data() {
        return {

        }
    }
}
</script>

<style>
#v-modal {
  padding: 0;
  text-align: left;
  font-size: 1.1em;
  border-radius: 20px;
  box-shadow: 1px 1px 20px 0 #aeaeae;
}
#v-modal header {
  padding: 1em 2em;
  text-align: left;
}
#v-modal .content {
padding: 1em 2em;
    text-align: left;
}
</style>
