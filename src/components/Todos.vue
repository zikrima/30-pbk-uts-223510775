<template>
    <div>
      <h1>To Do List</h1>
      <input type="text" v-model="tugasBaru" @keyup.enter="tambahTugas" placeholder="Tambah tugas baru..." />
      <br>
      <div v-if="tugasBelumSelesai.length === 0">
        <p>Tidak ada tugas yang belum selesai.</p>
      </div>
      <div v-else>
        <h2>Daftar Tugas</h2>
        <br>
        <button @click="filterBelumSelesai">{{ tampilkanBelumSelesaiSaja ? 'Tampilkan Semua' : 'Tampilkan Belum Selesai Saja' }}</button>
        <br><br>
        <div v-for="tugas in tugasBelumSelesai" :key="tugas.id">
          <div>
            <input type="checkbox" :id="'checkbox-' + tugas.id" v-model="tugas.completed" />
            <label :for="'checkbox-' + tugas.id">
              <span :class="{ 'completed': tugas.completed }">{{ tugas.text }}</span>
            </label>
            <button @click="hapusTugas(tugas)">Hapus</button>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
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
      hapusTugas(tugas) {
        this.daftarTugas = this.daftarTugas.filter(item => item.id !== tugas.id);
      },
      filterBelumSelesai() {
        this.tampilkanBelumSelesaiSaja = !this.tampilkanBelumSelesaiSaja;
      }
    }
  }
  </script>
  
  <style>
  .completed {
    text-decoration: line-through;
  }
  
  body {
    background-color: grey;
  }
  
  h1 {
    font-size: 24px;
    color: #333;
    margin-bottom: 20px;
  }
  
  input[type="text"] {
    padding: 8px;
    margin-bottom: 10px;
    width: 300px;
  }
  
  button {
    padding: 6px 12px;
    margin-left: 10px;
    cursor: pointer;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 4px;
  }
  
  button:hover {
    background-color: #45a049;
  }
  
  .task-item {
    margin-bottom: 10px;
  }
  
  .task-item label {
    cursor: pointer;
  }
  
  .completed {
    text-decoration: line-through;
  }
  
  .no-tasks {
    color: #888;
  }
  </style>
  