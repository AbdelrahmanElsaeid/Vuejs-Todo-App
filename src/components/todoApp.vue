<template>
  <div class ='container'>
    <h2 class="text-center mt-5">ToDo App</h2>
    <div class="d-flex mt-5">
      <input type="text" placeholder="Enter Task" class="w-100 form-control" v-model="task">
      <button class="btn btn-warning" @click="submitTask">Add</button>
    </div>
    <table class="table mt-5 table-bordered">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col">#</th>
          <th scope="col">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task,index) in tasks" :key="index">
          <th scope="row"> <span :class="{'finished': task.status=='finished'}">{{ task.name }} </span></th>
          <td><span @click="changeStatus(index)" class="pointer"  :class="{
            'text-danger' : task.status == 'todo',
            'text-success' : task.status == 'finished',
            'text-warning' : task.status == 'inprogress',
          }">{{ task.status }}</span></td>
          <td>
            <div @click="deleteTask(index)" class="pointer">
              <span class="fa fa-trash"></span>
            </div>
          </td>
          <td>
            <div @click="editTask(index)" class="pointer">
              <span class="fa fa-pen"></span>
            </div>
          </td>
        </tr>

      </tbody>
</table>  

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return{
      task: '',
      editedtask: null,
      availableStatus:['todo','inprogress','finished'],
      tasks : [
        {
          name: 'study programming',
          status: 'todo'
        },
        {
          name: 'study java',
          status: 'inprogress'
        }
      ]
    }
  },
  methods: {
    submitTask(){
      if (this.task==0) return;
      if (this.editedtask==null){
        this.tasks.push({
        name:this.task,
        status: 'todo'
      })

      }
      else{
        this.tasks[this.editedtask].name = this.task
        this.editedtask = null ;

      }
      
      this.task ='';
    },
    deleteTask(index){
      this.tasks.splice(index,1)
    },
  
    editTask(index){
      this.task = this.tasks[index].name;
      this.editedtask= index;

    },
    changeStatus(index){
      let newIndex = this.availableStatus.indexOf(this.tasks[index].status)
      if (++newIndex > 2) newIndex=0
      this.tasks[index].status = this.availableStatus[newIndex]
    },



  }
}
</script>

<style>
  .pointer{
    cursor: pointer;

  }
  .finished{
    text-decoration: line-through;
  }
</style>


