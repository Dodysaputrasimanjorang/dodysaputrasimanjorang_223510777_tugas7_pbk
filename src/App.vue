~<template>
  <div id="app">
    <h1>Aplikasi Daftar Tugas</h1>
    <TaskList />
  </div>
</template>

<script>
import TaskList from './components/TaskList.vue';

export default {
  components: {
    TaskList,
  },
};
</script>

<style>
body {
  font-family: 'Arial', sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f9f9f9;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#app {
  max-width: 600px;
  margin: 20px;
  padding: 20px;
  background-color: white;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
}

h1 {
  font-size: 2em;
  text-align: center;
  margin-bottom: 20px;
  color: #333;
}
</style>
