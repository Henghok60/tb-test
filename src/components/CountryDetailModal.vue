<template>
  <b-modal :id="'modal-' + index" :title="item.name.official" hide-footer>
    <p class="my-4">Name : {{ item.name.official }}</p>
    <p class="my-4">CCA2 : {{ item.cca2 }}</p>
    <p class="my-4">CCA3 : {{ item.cca3 }}</p>
    <p class="my-4">CCA3 : {{ item.cca3 }}</p>
    <p class="my-4">CIOC : {{ item.cioc }}</p>
    <p class="my-4">Independent : {{ item.independent }}</p>
    <p class="my-4">Status : {{ item.status }}</p>
    <p class="my-4">UN memeber : {{ item.unMember }}</p>
    <p class="my-4">Region : {{ item.region }}</p>
    <p class="my-4">Sub Region : {{ item.subregion }}</p>
    <span>Language : </span><span v-for=" (value, key) in item.languages" v-bind:key="key">{{value}} , </span>
    <p class="my-4">Population : {{ item.population }}</p>

  </b-modal>
</template>

<script>
export default {
  props: ["item", "index"],
};
</script>
