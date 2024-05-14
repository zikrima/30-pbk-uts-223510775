<template>
    <div>
      <h1>Postingan User</h1>
      <div>
        <label for="user-select">Pilih User:</label>
        <select id="user-select" v-model="selectedUser" @change="fetchPosts">
          <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
        </select>
      </div>
      <div v-if="posts.length === 0">
        <p>Tidak ada postingan untuk user ini.</p>
      </div>
      <div v-else>
        <h2>Daftar Postingan</h2>
        <ul>
          <li v-for="post in posts" :key="post.id">
            <h3>{{ post.title }}</h3>
            <p>{{ post.body }}</p>
          </li>
        </ul>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        users: [],
        posts: [],
        selectedUser: null
      };
    },
    mounted() {
      this.fetchUsers();
    },
    methods: {
      async fetchUsers() {
        try {
          const response = await fetch('https://jsonplaceholder.typicode.com/users');
          this.users = await response.json();
        } catch (error) {
          console.error('Error fetching users:', error);
        }
      },
      async fetchPosts() {
        if (!this.selectedUser) return;
        try {
          const response = await fetch(`https://jsonplaceholder.typicode.com/posts?userId=${this.selectedUser}`);
          this.posts = await response.json();
        } catch (error) {
          console.error('Error fetching posts:', error);
        }
      }
    }
  };
  </script>
  
  <style>
  h1 {
    font-size: 24px;
    color: #333;
    margin-bottom: 20px;
  }
  
  label {
    margin-right: 10px;
  }
  
  select {
    padding: 5px;
    border-radius: 4px;
    border: 1px solid #ccc;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    margin-bottom: 20px;
  }
  
  h3 {
    margin: 0;
    font-size: 20px;
    color: #333;
  }
  
  p {
    margin: 5px 0 0;
    color: #666;
  }
  </style>
  