<template>
  <div>
    <label for="user-select">Pilih User:</label>
    <select id="user-select" v-model="selectedUser" @change="fetchPosts">
      <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
    </select>
    <div v-if="posts.length > 0">
      <div v-for="post in posts" :key="post.id" class="post">
        <h3>{{ post.title }}</h3>
        <p>{{ post.body }}</p>
      </div>
    </div>
    <div v-else>
      <p>Tidak ada postingan untuk user ini.</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      users: [],
      selectedUser: null,
      posts: []
    };
  },
  created() {
    this.fetchUsers();
  },
  methods: {
    fetchUsers() {
      axios.get('https://jsonplaceholder.typicode.com/users')
        .then(response => {
          this.users = response.data;
        })
        .catch(error => {
          console.error("Ada masalah saat mengambil data users:", error);
        });
    },
    fetchPosts() {
      if (this.selectedUser) {
        axios.get(`https://jsonplaceholder.typicode.com/posts?userId=${this.selectedUser}`)
          .then(response => {
            this.posts = response.data;
          })
          .catch(error => {
            console.error("Ada masalah saat mengambil data posts:", error);
          });
      } else {
        this.posts = [];
      }
    }
  }
};
</script>

<style scoped>
.post {
  border-bottom: 1px solid #ddd;
  padding: 10px 0;
}
h3 {
  margin: 0;
}
</style>
