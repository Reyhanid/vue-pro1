<!-- <script>
export default{
  data(){
    return {
      name: 'reyhoon',
      status: 'busy',
      tasks:['task one', 'task two', 'task three'],
      link:'https://google.com'
    };
  },
  methods:{
    toggleStatus(){
      if(this.status === 'programming'){
        this.status='busy';
      }
      else if(this.status === 'busy'){
        this.status='not programming';
      }
      else {
        this.status='programming'
      }
    }
  },
};
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'programming'">this user is programming!</p>
  <p v-else-if="status === 'busy'">this user is busy</p>
  <p v-else>this user is not programming</p>

  <h3>tasks:</h3>
  <ul>
    <li v-for="task in tasks" :key="task" >{{ task }}</li>
  </ul>

  <!-- <a v-bind:href="link">Click for google</a> -->
  <!-- <a :href="link">Click for google</a>
  <br>
  <br> -->
  <!-- <button v-on:click="toggleStatus">Change Status</button> -->
   <!-- <button @click="toggleStatus">Change Status</button>
</template>

<style scoped></style> -->

<!-- <-- -------------------------------------------------------------------------------------------- -->
<script setup>

import {ref , onMounted} from 'vue';

    const name=ref('Reyhoon');
    const status=ref ('busy');
    const tasks=ref (['Task one','Task two','Task three']);
    const newTask=ref(' ');

    const toggleStatus = () =>{
      if(status.value === 'programming'){
        status.value='busy';
      }
      else if(status.value === 'busy'){
        status.value='not programming';
      }
      else {
        status.value='programming'
      }
    }


    const addTask = () =>{
      if(newTask.value.trim() !== ''){
        tasks.value.push(newTask.value);
        newTask.value = '';
      }
    }

    const deleteTask = (index)=>{
      tasks.value.splice(index,1);
    }


    onMounted(async () => {
    try {
      const response = await fetch('https://jsonplaceholder.typicode.com/todos');
      const data = await response.json();
      tasks.value = data.map((task) => task.title);
    } catch (error) {
      console.log('Error fetching tasks');
    }
    });
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'programming'">this user is programming!</p>
  <p v-else-if="status === 'busy'">this user is busy</p>
  <p v-else>this user is not programming</p>

  <form @submit.prevent="addTask">
    <label for="addTask">Add Task</label>
    <input type="text" id="addTask" name="addTask" v-model="newTask">
    <button type="submit">submit</button>
  </form>

  <h3>tasks:</h3>
  <ul>
    <li v-for="(task , index) in tasks" :key="task" >
      <span>
        {{ task }}
      </span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>

  <br>
  <br>
  <!-- <button v-on:click="toggleStatus">Change Status</button> -->
   <button @click="toggleStatus">Change Status</button>
</template>

<style scoped></style>
