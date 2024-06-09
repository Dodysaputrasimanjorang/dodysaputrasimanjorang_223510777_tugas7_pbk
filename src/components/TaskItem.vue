<template>
  <li :class="{ completed: task.completed }">
    <div class="task-item">
      <input type="checkbox" :checked="task.completed" @change="toggleTask" />
      <span>{{ task.name }}</span>
    </div>
    <button @click="removeTask">Hapus</button>
  </li>
</template>

<script>
export default {
  props: {
    task: Object,
  },
  methods: {
    toggleTask() {
      this.$emit('toggle-task', this.task.id);
    },
    removeTask() {
      this.$emit('remove-task', this.task.id);
    },
  },
};
</script>

<style scoped>
li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #ddd;
}
.completed span {
  text-decoration: line-through;
  color: #aaa;
}
.task-item {
  display: flex;
  align-items: center;
}
input[type="checkbox"] {
  margin-right: 10px;
}
button {
  background-color: #ff6b6b;
  border: none;
  padding: 5px 10px;
  color: white;
  border-radius: 4px;
  cursor: pointer;
}
button:hover {
  background-color: #ff4c4c;
}
</style>
