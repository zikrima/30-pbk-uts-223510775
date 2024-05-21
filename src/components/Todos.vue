<template>
  <div>
    <h1>To Do List</h1>
    <input type="text" v-model="tugasBaru" @keyup.enter="tambahTugas" placeholder="Tambah tugas baru..." />
    <br>
    <ToDoList :tugasList="tugasBelumSelesai" @toggle-status="toggleStatus" @hapus-item="hapusItem" />
    <br>
    <button @click="filterBelumSelesai">{{ tampilkanBelumSelesaiSaja ? 'Tampilkan Semua' : 'Tampilkan Belum Selesai Saja' }}</button>
  </div>
</template>

<script>
import ToDoList from './ToDoList.vue';

export default {
  components: {
    ToDoList
  },
  data() {
    return {
      tugasBaru: '',
      daftarTugas: [],
      tampilkanBelumSelesaiSaja: false
    };
  },
  computed: {
    tugasBelumSelesai() {
      if (this.tampilkanBelumSelesaiSaja) {
        return this.daftarTugas.filter(tugas => !tugas.completed);
      }
      return this.daftarTugas;
    }
  },
  methods: {
    tambahTugas() {
      if (this.tugasBaru.trim() !== '') {
        this.daftarTugas.push({ id: Date.now(), text: this.tugasBaru, completed: false });
        this.tugasBaru = '';
      }
    },
    toggleStatus(tugas) {
      const index = this.daftarTugas.findIndex(item => item.id === tugas.id);
      if (index !== -1) {
        this.daftarTugas[index].completed = !this.daftarTugas[index].completed;
      }
    },
    hapusItem(tugas) {
      this.daftarTugas = this.daftarTugas.filter(item => item.id !== tugas.id);
    },
    filterBelumSelesai() {
      this.tampilkanBelumSelesaiSaja = !this.tampilkanBelumSelesaiSaja;
    }
  }
};
</script>

<style>
.completed {
  text-decoration: line-through;
}
</style>
