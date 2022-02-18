<template>
<div id="c-modal">
<label for="modal_1" class="button">?</label>
  <div class="modal">
  <input id="modal_1" type="checkbox" />
  <label for="modal_1" class="overlay"></label>
  <div>
    <header>
      <h3>Great offer</h3>
      <label for="modal_1" class="close">&times;</label>
    </header>
    <section class="content">
      We have a special offer for you. I am sure you will love it! However this does look spammy...
    </section>

  </div>
</div>
</div>
</template>

<script>
export default {
    name: 'Modal',
    props: ['class', 'label', 'msg'],

}
</script>

<style>

</style>
