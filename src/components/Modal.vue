<template>
<div id="c-modal">
<label for="modal_1" class="button">{{ lab }}</label>
  <div class="modal">
  <input id="modal_1" type="checkbox" />
  <label for="modal_1" class="overlay"></label>
  <div id="v-modal">
    <header>
      <h3>{{ lab }}</h3>
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
    props: ['lab', 'msg'],
    data() {
        return {

        }
    }
}
</script>

<style>
#v-modal {
    padding: 2em;
    /* text-align: center; */
    font-size: 1.1em;
}
</style>
