<template>
  <div class="hello">
    <div class="container col-sm-8 col-sm-offset-2 mt-5">
      <div id="taskApp">
        <div class="panel panel-default">
          <h2 class='text-center mb-3'>Add New Task</h2>
          <form v-on:submit='addTask'>
            <div class=" input-group mb-5 ">
              <input type="text" class='form-control ' v-model='tasks.name'>
              <div class="input-group-append">
              <input type="submit" value='Add' class='btn btn-primary btn-block'>
            </div>
            </div>
          </form>
          &nbsp;
        </div>
      <table class="table">
        <thead class="thead-dark">
        <tr>
          <th scope="col">Checkmark Done</th>
          <th scope="col">Task</th>
          <th scope="col">Delete</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="task in tasks" :key="task">
          <td><input type="checkbox" v-model="task.done"></td>
          <td><span :class="{ taskDone: task.done }">{{ task.name }}</span></td>
          <td><button class="btn btn-danger btn-block" v-on:click="deleteTask(task)">Delete</button></td>
        </tr>
        </tbody>
      </table>
    </div>
  </div>
  </div>
</template>

<script>
const STORAGE_KEY='tastk-storage';
export default {
  name: 'HelloWorld',
  data() {
    return {
      tasks: [
        {name: 'my first task', done: false},

      ],
    }
  },
  created() {
    this.tasks = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]')
  },
  methods:{
    addTask: function(e) {
      e.preventDefault();
      this.tasks.push({
        name: this.tasks.name,
        done: false
      });
      localStorage.setItem(STORAGE_KEY,JSON.stringify(this.tasks))
    },
    deleteTask: function(task) {
      this.tasks.splice(this.tasks.indexOf(task), 1)
      localStorage.setItem(STORAGE_KEY,JSON.stringify(this.tasks))
    },
  }

}
</script>


<style scoped>
.hello{
  width: 80%;
  margin-left: 10%;
  height: 80%;
  background-color:#545b621f;
}
</style>