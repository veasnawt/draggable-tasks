<template>
  <div id="app">
      <h1 class="app-title">Draggable Tasks</h1>
      <input type="text" class="new-task" v-model="newTask" placeholder="New Task" @keyup.enter="add"/>
      <select class="task-status" v-model="taskStatus">
        <option value="" selected disabled hidden>Task Status</option>
        <option value="todoTask">To Do</option>
        <option value="inProgressTask">In Progress</option>
        <option value="testingTask">Testing</option>
        <option value="doneTask">Done</option>
      </select>
      <button class="add" @click="add">Add</button>
    <br/>
    <div id="tasks-area">
      <div class="task-wrapper todo">
        <div class="task-type">To Do</div><br/>
          <draggable class="tasks" :list="todoTasks" group="tasks">
           <div class="task" v-for="element in todoTasks" :key="element.name">
             <p class="task-title">
               {{element.name}}
             </p>
           </div>
          </draggable>
      </div>
      <div class="task-wrapper in-progress">
        <div class="task-type">In Progress</div><br/>
          <draggable class="tasks" :list="inProgressTasks" group="tasks">
           <div class="task" v-for="element in inProgressTasks" :key="element.name">
             <p class="task-title">
               {{element.name}}
             </p>
           </div>
          </draggable>
      </div>
      <div class="task-wrapper testing">
        <div class="task-type">Testing</div><br/>
          <draggable class="tasks" :list="testingTasks" group="tasks">
           <div class="task" v-for="element in testingTasks" :key="element.name">
             <p class="task-title">
               {{element.name}}
             </p>
           </div>
          </draggable>
      </div>
      <div class="task-wrapper done">
        <div class="task-type">Done</div><br/>
          <draggable class="tasks" :list="doneTasks" group="tasks">
           <div class="task" v-for="element in doneTasks" :key="element.name">
             <p class="task-title">
               {{element.name}}
             </p>
           </div>
          </draggable>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: 'App',
  components: {
    // eslint-disable-next-line vue/no-unused-components
    draggable
  },
  data() {
    return {
      newTask: "",
      taskStatus: "",
      todoTasks: [
        // {name: "Task 1"},
        // {name: "Task 2"},
        // {name: "Task 3"},
        // {name: "Task 4"},
      ],
      inProgressTasks: [],
      testingTasks: [],
      doneTasks: [],
    }
  },
  methods: {
    add() {
      if(this.newTask) {
        switch(this.taskStatus) {
          case "todoTask":
            this.todoTasks.push({name: this.newTask});
            break;
          case "inProgressTask":
            this.inProgressTasks.push({name: this.newTask});
            break;
          case "testingTask":
            this.testingTasks.push({name: this.newTask});
            break;
          case "doneTask":
            this.doneTasks.push({name: this.newTask});
            break;
          default:
            this.todoTasks.push({name: this.newTask});
        }
        this.newTask = "";
        this.taskStatus = "";
      }
    }
  }
}
</script>

<style>

  html, body {
    height: 100%;
    margin: 0;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: #efefef;

  }
  #app {
    margin: 30px;
  }

  .app-title {
    background: -webkit-linear-gradient(#0debff, #f22dff);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    padding: 50px 0;
    text-align: center;
    text-transform: uppercase;
  }

  .new-task, .task-status, .add {
    width: 270px;
    height: 45px;
    font-size: 20px;
    padding-left: 20px;
    padding-right: 20px;
    box-sizing: border-box;
    border-radius: 7px;
    margin-right: 15px;
    margin-bottom: 15px;
    background: #fff;
    border-color: transparent;
    outline: none;
  }

  .add {
    width: 100px !important;
    background: #f22dff;
    border-color: #f22dff;
    border: none;
  }

  .add:hover {
    background: #0debff;
  }

  #tasks-area {
    padding: 30px 0;
    padding-top: 15px;
    display: flex;
    align-content: flex-start;
    flex-flow: row wrap;
    gap: 15px;
  }

  .task-wrapper {
    flex: 1;
    min-height: 400px;
    min-width: 270px;
    max-width: 270px;
    padding: 20px;
    background: #fff;
    border-radius: 7px;
  }

  .task-type {
    text-align: center;
    text-transform: uppercase;
  }

  .tasks {
    min-height: 400px;
  }

  .task {
    position: relative;
    width: 230px;
    height: 45px;
    background: rgb(13,235,255);
    background: linear-gradient(90deg, rgba(55,167,255,1) 0%, rgba(13,235,255,1) 100%);
    margin-bottom: 5px;
    padding: 0 20px;
    border-radius: 5px;
    box-shadow: 1px 1px 4px #c5c5c5;
  }

  .task-title {
    margin: 0;
    position: absolute;
    top: 50%;
    transform: translate(0, -50%);
    color: #fff;
  }

  .task-title:hover {
    cursor: grab;
  }

</style>
