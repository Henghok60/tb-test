<template>
  <div>
    <div class="row mt-1">
      <div class="col-1">
        <img :src="item.flags.png" alt="" class="w-5" />
      </div>
      <div class="col-3">
        <span v-b-modal="modalId(index)">{{ item.name.official }}</span>
      </div>
      <div class="col-1">
        <span>{{ item.cca2 }} </span>
      </div>
      <div class="col-1">
        <span>{{ item.cca3 }}</span>
      </div>
      <div class="col-3">
        <span v-for="element in item.altSpellings" v-bind:key="element">
          {{ element }}
        </span>
      </div>
      <div class="col-2">
        <span v-for="element in item.idd.suffixes" v-bind:key="element">
          {{ item.idd.root }}{{ element }},
        </span>
      </div>
    </div>

    <CountryDetailModal :item="item" :index="index"></CountryDetailModal>
  </div>
</template>

<script>
import CountryDetailModal from './CountryDetailModal.vue';

export default {
    props: ["item" , "index"],
    methods: {
        modalId: (id) => {
            return "modal-" + id;
        },
    },
    components: { CountryDetailModal }
};
</script>
