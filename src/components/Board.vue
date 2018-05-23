<template>
  <div class="row">

    <AddTask @createTask="createTask" />

    <Panel class ="ToDo" title= "ToDo" @deleteTask="deleteTask" @moveRight="moveRight" :tasks="ToDo" />
    <Panel class ="Doing" title= "Doing" @deleteTask="deleteTask" @moveLeft="moveLeft" @moveRight="moveRight" :tasks="Doing" />
    <Panel class ="Review" title= "Review" @deleteTask="deleteTask" @moveLeft="moveLeft" @moveRight="moveRight" :tasks="Review" />
    <Panel class ="Done" title= "Done" @deleteTask="deleteTask" @moveLeft="moveLeft" @moveRight="moveRight" :tasks="Done" />

  </div>
</template>

<script>
  import AddTask from '@/components/AddTask'
  import Panel from '@/components/Panel'
  import * as firebase from 'firebase'
  const config = {
    apiKey: "AIzaSyArzac8M__7lw7uIDzjySBs7M1qGJb8mAU",
    authDomain: "mykanban-c14ea.firebaseapp.com",
    databaseURL: "https://mykanban-c14ea.firebaseio.com",
    projectId: "mykanban-c14ea",
    storageBucket: "mykanban-c14ea.appspot.com",
    messagingSenderId: "130315909149"
  }
  const firebaseApp = firebase.initializeApp(config)
  const db = firebaseApp.database()
  const tasksRef = db.ref('tasks')
  export default {
    components: {
      AddTask,
      Panel
    },
    firebase: {
      tasks: tasksRef
    },
    name: 'board',
    computed: {
      ToDo () {
        return this.tasks.filter(task => task.status === 0);
      },
      Doing () {
        return this.tasks.filter(task => task.status === 1);
      },
      Review () {
        return this.tasks.filter(task => task.status === 2);
      },
      Done () {
        return this.tasks.filter(task => task.status === 3);
      }
    },
    methods: {
      createTask (newTask) {
        tasksRef.push(newTask);
      },
      deleteTask (task) {
        tasksRef
          .child(task['.key'])
          .remove();
      },
      moveLeft (task) {
        tasksRef
          .child(task['.key'])
          .child('status')
          .set(task['status'] - 1);
      },
      moveRight (task) {
        tasksRef
          .child(task['.key'])
          .child('status')
          .set(task['status'] + 1);
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.Review{
  width: 250px;
  height: 100%;
  border-left: 2px solid black;
  border-right: 2px solid black;
  background: burlywood;
  float: left;
  margin-right: 10px;
  text-align: center;
  padding:0px
}

.Doing{
  width: 250px;
  height: 100%;
  border-left: 2px solid black;
  border-right: 2px solid black;
  background: darkgray;
  float: left;
  margin-right: 10px;
  text-align: center;
  padding: 0px
}

.Done{
  width: 250px;
  height: 100%;
  border-left: 2px solid black;
  border-right: 2px solid black;
  background: darkseagreen;
  float: left;
  margin-right: 10px;
  text-align: center;
  padding: 0px
}

.ToDo{

  width: 250px;
  height: 100%;
  border-left: 2px solid black;
  border-right: 2px solid black;
  background: darkcyan;
  float: left;
  margin-right: 10px;
  text-align: center;
  padding: 0px
}

.row{
  margin:0% auto;
  display: table;
}

title{
  
}
</style>
