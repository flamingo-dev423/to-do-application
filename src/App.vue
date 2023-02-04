<template>
<h1 class="text-2xl font-semibold text-gray-900 ">My Vue to-do App</h1>

  <todoApp/>
  <router-view/>
</template>

<script>
import todoApp from './components/todoapp.vue'

export default {
  name: 'App',
  components: {
    todoApp
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Fira+Code:wght@200;300;400;500;600&display=swap');
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
