<template>
  <div class="container">
    <Header
      title="Task Tracker"
      :showAddTask="showAddTask"
      @show-add-task="onShowAddTask"
    />
    <div v-show="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
    <Tasks
      @toggle-reminder="toggleReminder"
      :tasks="tasks"
      @delete-task="deleteTask"
    />
  </div>
</template>

<script>
import AddTask from './components/AddTask.vue';
import Header from './components/Header.vue';
import Tasks from './components/Tasks.vue';

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask,
  },

  data() {
    return {
      tasks: [],
      showAddTask: false,
    };
  },

  methods: {
    addTask(task) {
      this.tasks = [...this.tasks, task];
    },

    deleteTask(taskId) {
      const deletedTask = this.tasks.filter((task) => task.id !== taskId);

      this.tasks = deletedTask;
    },

    toggleReminder(taskId) {
      this.tasks = this.tasks.map((task) =>
        task.id === taskId ? { ...task, reminder: !task.reminder } : task
      );
    },

    onShowAddTask() {
      this.showAddTask = !this.showAddTask;
    },
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Task 1',
        day: new Date().toLocaleString('pt-br'),
        reminder: true,
      },
      {
        id: 2,
        text: 'Task 2',
        day: new Date().toLocaleString('pt-br'),
        reminder: true,
      },
      {
        id: 3,
        text: 'Task 3',
        day: new Date().toLocaleString('pt-br'),
        reminder: false,
      },
    ];
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}

.btn-block {
  display: block;
  width: 100%;
}
</style>
