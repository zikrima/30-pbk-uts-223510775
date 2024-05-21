<template>
  <div>
    <header>
      <nav>
        <button @click="menu = 'todos'">Todos</button>
        <button @click="menu = 'posts'">Posts</button>
      </nav>
    </header>
    <main>
      <Todos v-if="menu === 'todos'" />
      <Posts v-if="menu === 'posts'" />
    </main>
  </div>
</template>

<script>
import Todos from './components/Todos.vue';
import Posts from './components/Posts.vue';

export default {
  components: {
    Todos,
    Posts
  },
  data() {
    return {
      menu: 'todos'
    };
  }
};
</script>

<style>
header {
  background-color: #333;
  padding: 10px;
}
nav {
  display: flex;
  justify-content: space-around;
}
button {
  padding: 10px;
  cursor: pointer;
  color: white;
  background-color: #4CAF50;
  border: none;
  border-radius: 4px;
}
button:hover {
  background-color: #45a049;
}
</style>
