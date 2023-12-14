<script>
import index from './components/index.vue';
import create from './components/create.vue';

export default {
  components: {
    index,
    create,
  },
  data() {
    return {
      showIndex: true,
    };
  },
  methods: {
    toggleComponents() {
      this.showIndex = !this.showIndex;
    },
  },
};

</script>

<template>
  <button @click="toggleComponents">
    {{ showIndex ? 'Aggiugi una Pizza' : 'Mostra Index' }}
  </button>
  <index v-if="showIndex"></index>
  <create v-if="!showIndex"></create>
</template>

<style></style>
