<template>
  <div>
    <input type="checkbox" v-model="todo.completed" />
    <span :style="{ 'text-decoration': todo.completed ? 'line-through' : 'none' }">{{ todo.text }}</span>
    <button @click="hapusTugas">Hapus</button>
  </div>
</template>

<script>
export default {
  props: ['todo'],
  methods: {
    hapusTugas() {
      this.$emit('hapus-item', this.todo);
    }
  }
};
</script>

<style scoped>
span {
  cursor: pointer;
}
</style>