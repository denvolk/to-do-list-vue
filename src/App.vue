<template>
  <div class="todo-list">
    <form class="form" v-on:submit.prevent="addTask">
      <input v-model="newTask" name="newTask" placeholder="Название задачи" size="100" id="newTask">
      <button type="submit">Добавить задачу</button>
    </form>
    <div class="task-list">
      <div class="task" v-for="task in tasks" v-bind:key="task.id">
        <input type="checkbox" v-model="task.completed">
        <span v-bind:class="{completed: task.completed}">{{task.name}}</span>
        <img src="./pics/bin.png" alt="bin.png" v-on:click="removeTask(task)">
      </div>
    </div>
  </div>
</template>

<script>
//import {ref} from 'vue';

export default {
  data: {
    newTask: '',
    tasks: []
  },

  methods: {
    addTask() {
      if (!this.newTask.trim())
        this.newTask = 'Название задания ' + Date.now();

      this.tasks.push({
        name: this.newTask,
        completed: false
      });
      this.newTask = '';
    },

    removeTask(task)  {
      const index = this.tasks.indexOf(task);
      this.tasks.splice(index, 1);
    }
  }
}
</script>

<style>
.completed {
  text-decoration-line: line-through;
}
</style>
