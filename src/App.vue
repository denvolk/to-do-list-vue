<template>
  <div class="todo-list">
    <form v-on:submit.prevent="addTask">
      <button>Добавить задачу</button>
      <input v-model="newTask" name="newTask" placeholder="Название задачи" size="100">
    </form>
    <div class="task-list">
      <div v-for="task in tasks" v-bind:key="task.id" v-bind:class="{completed: task.completed}" class="task">
        <input type="checkbox" v-on:change="setCompleted(task)">
        {{ task.name }}
        <img src="../src/pics/bin.png" v-on:click="removeTask(task)" alt="bin.png">
      </div>
    </div>
  </div>
</template>

<script>
import {ref} from 'vue';

export default {
  setup() {
    const newTask = ref('');
    const tasks = ref([]);

    function addTask() {
      if (!newTask.value.trim())
        newTask.value += "Название задачи " + Date.now();

      tasks.value.push({
        id: Date.now(),
        name: newTask.value,
        completed: false,
      });

      newTask.value = '';
    }

    function setCompleted(todo) {
      todo.completed = !todo.completed;
    }

    function removeTask(task) {
      console.log(task.id);

      let index = tasks.value.map(function (e) {
        return e.id;
      }).indexOf(task.id);

      console.log(index);

      tasks.value.splice(index, 1);
    }

    /*function genTasks() {
      for (let iter = 0; iter < 6; iter++)  {
        newTask.value = (iter + 1).toString();
        setTimeout(addTask, 1000);
      }
    }*/


    return {
      tasks,
      newTask,

      addTask,
      setCompleted,
      removeTask,
      //genTasks,
    };
  }
}
</script>

<style>
.completed {
  text-decoration-line: line-through;
}
</style>
