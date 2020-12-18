<template>
  <div class="home">
    <div class="taskInputs">
      <label
        >Task Name:
        <input type="text" v-model="taskName" />
      </label>

      <button class="taskButton addButton" @click="addTodo(taskName)">Add Task</button>
      <button class="taskButton clearButton" @click="clearAllTasks()">Clear All Tasks</button>
    </div>

    <span id=taskError v-if='showError'> {{ taskNameError }} </span>

    <div class="todoTableContainer">
      <table class="todoTable">
        <thead>
          <tr>
            <th style='width: 75px;'>ID</th>
            <th style='width: 350px;'>Name</th>
            <th style='width: 75px; padding-left: 3px; padding-right: 3px'>Completed</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="d in todo" :key="d.id">
            <td>{{ d.id }}</td>
            <td>{{ d.taskName }}</td>
            <td><input type="checkbox" v-bind:checked="d.completed" /></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>
.todoTableContainer {
  overflow-y: auto;
  border: 4px double black;
  max-height: 200px;
  width: 500px;
  margin-top: 10px;
}

.todoTable th {
  border-bottom: 2px double black;
  position: sticky;
  top: 0px;
  z-index: 2;
  background-color: #737b83;
  color: white;
}

.taskButton {
  margin-left: 5px;
}

.taskInputs {
  margin-top: 5px;
}

.addButton {
    color: white;
  background-color: green;
  border: 2px ridge green;
  box-shadow: 1px 1px 1px 1px lightgray;
  border-radius: 3px;
}

.clearButton {
  color: white;
  background-color: red;
  border: 2px ridge red;
  box-shadow: 1px 1px 1px 1px lightgray;
  border-radius: 3px;
}

#taskError {
  margin-top: 5px;
  color: red;
  font-weight: bold;
}
</style>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component({})
export default class Home extends Vue {
  curId = 1;
  taskName = ''
  showError = false
  taskNameError = 'Please enter a valid task name.'
  todo: Array<{
    id: number;
    taskName: string;
    completed: boolean;
  }> = [];

  addTodo(taskName: string) {
    const found = this.todo.findIndex(f => f.taskName === taskName)
    if(taskName.length > 0 && found === -1) {
      this.todo = [...this.todo, { id: this.curId, taskName, completed: false }];
      this.curId += 1;
      this.taskName = ''
    } else {
      this.showError = true
      setTimeout(() => this.showError = false, 3000)
    }
  }

  deleteTodo(id: number) {
    const newT = this.todo.filter((t) => t.id !== id);
    this.todo = [...newT];
    this.$props.numToDo(this.todo.length);
  }

  updateCompleted(id: number) {
    this.todo = [];
  }

  clearAllTasks() {
    const x = prompt("You are about to clear all tasks. To confirm, type DELETE.");
    if(x === 'DELETE' || x === 'delete') {
      this.todo = []
      this.curId = 1
    }
  }
}
</script>
