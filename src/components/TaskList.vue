<template>
  <div class="task-list-container">
    <h2>Daftar Tugas</h2>
    <ul>
      <TaskItem
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @toggle-task="toggleTask"
        @remove-task="removeTask"
      />
    </ul>
    <div class="task-summary">
      <p>Jumlah tugas yang belum selesai: {{ incompleteTasksCount }}</p>
    </div>
    <div class="task-input">
      <input v-model="newTaskName" @keyup.enter="addTask" placeholder="Nama tugas baru" />
      <button @click="addTask">Tambah Tugas</button>
    </div>
  </div>
</template>

<script>
import { ref, computed } from 'vue';
import { useTaskStore } from '../stores/taskStore';
import TaskItem from './TaskItem.vue';

export default {
  components: { TaskItem },
  setup() {
    const taskStore = useTaskStore();
    const newTaskName = ref('');

    const tasks = computed(() => taskStore.tasks);
    const incompleteTasksCount = computed(() => taskStore.incompleteTasksCount);

    const addTask = () => {
      if (newTaskName.value.trim()) {
        taskStore.addTask({
          id: Date.now(),
          name: newTaskName.value,
          completed: false,
        });
        newTaskName.value = '';
      }
    };

    const toggleTask = (taskId) => {
      taskStore.toggleTask(taskId);
    };

    const removeTask = (taskId) => {
      taskStore.removeTask(taskId);
    };

    return {
      newTaskName,
      tasks,
      incompleteTasksCount,
      addTask,
      toggleTask,
      removeTask,
    };
  },
};
</script>

<style scoped>
.task-list-container {
  padding: 20px;
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}
h2 {
  margin-bottom: 20px;
  color: #333;
}
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
.task-summary {
  margin-top: 20px;
  font-weight: bold;
  color: #333;
}
.task-input {
  margin-top: 20px;
  display: flex;
}
input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  margin-right: 10px;
}
button {
  padding: 10px 20px;
  background-color: #4CAF50;
  border: none;
  color: white;
  border-radius: 4px;
  cursor: pointer;
}
button:hover {
  background-color: #45a049;
}
</style>
