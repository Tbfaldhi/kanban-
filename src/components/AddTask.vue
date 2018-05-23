<template>
  <div class="col-lg-12">
    <div class="row">
      <div class="col-lg-3">
        <h3>Add a Task</h3>
        <form v-on:submit.prevent="createTask">
          <input type="text" v-model="newTask.title" name="title" class="form-control" placeholder="Title" autofocus required>
          
          <input type="number" v-model="newTask.points" name="points" class="form-control" placeholder="Points" required>
          
          <input type="text" v-model="newTask.assigned_to" name="assigned_to" class="form-control" placeholder="Assigned To" required>
          <div>
          <button type="submit" class="btn btn-primary ">Submit</button>
          </div>
        </form>
      </div>
    </div>
    <hr>
  </div>
</template>

<script>
  export default {
    name: 'AddTask',
    data () {
      return {
        newTask: {
          title: '',
          points: 0,
          assigned_to: '',
          status: 0
        }
      }
    },
    methods: {
      createTask () {
        this.$emit('createTask', this.newTask);
        // Reset form
        this.newTask.title = '';
        this.newTask.points = 0;
        this.newTask.assigned_to = '';
      }
    }
  }
</script>

<style scoped>
  input {
    margin-bottom: 15px;
  }

  
</style>