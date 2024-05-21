<template>
  <div>
    <h2>Daftar Tugas</h2>
    <div v-for="tugas in tugasList" :key="tugas.id">
      <ToDoItem :todo="tugas" @toggle-status="toggleStatus" @hapus-item="hapusItem" />
    </div>
  </div>
</template>

<script>
import ToDoItem from './ToDoItem.vue';

export default {
  components: {
    ToDoItem
  },
  props: ['tugasList'],
  methods: {
    toggleStatus(tugas) {
      this.$emit('toggle-status', tugas);
    },
    hapusItem(tugas) {
      this.$emit('hapus-item', tugas);
    }
  }
};
</script>
