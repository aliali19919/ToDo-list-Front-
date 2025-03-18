<template >
    <section class="min-h-svh overflow-x-auto my-[150px]">
  <table class="table table-zebra">
   
    <thead>
      <tr class="text-2xl font-serif">
        <th>ID</th>
        <th>Task📝</th>
        <th>Competed✔️</th>
        <th>Actions🎬</th>
      </tr>
    </thead>
    <tbody>
  
      <tr v-for="task in tasks" class="text-lg font-mono">
        <th>{{ task.id }}</th>
        <td>{{ task.task }}</td>
        <td><form  method="post">
            <input type="checkbox">
        </form>
    </td>
<td>
        <button @click="deleteTask(task.id)"  class="btn btn-warning text-2xl w-[100px] h-[70px] md:w-[200px] md:h-[50px]  font-bold transition-all duration-200 hover:scale-105 hover:btn-error">Delete Task</button>
        
</td>
      </tr>
     
    </tbody>
  </table>
    </section>
</template>
<script>
import router from '@/router';
import axios from 'axios';
import Swal from 'sweetalert2';
import { onMounted, ref } from 'vue';

export default {
 setup(){

let deleteTask=(id)=>{
  Swal.fire({title:"Are You Sure You Want To Delete The Task ⚠️",icon:"warning",showCancelButton:true}).then((res)=>{
    if(res.isConfirmed){
  axios.delete(`http://127.0.0.1:8000/api/tasks/${id}`)
  tasks.value=tasks.value.filter((task)=>{return task.id!==id})
  
    }
  })
}

let tasks =ref([])
 onMounted(async ()=>{
  let response= await axios.get("http://127.0.0.1:8000/api/tasks");
  tasks.value=response.data
 })

 return{tasks,deleteTask}
 }
}
</script>
