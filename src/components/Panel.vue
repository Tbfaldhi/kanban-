<template>
  <div>
    <div class="col-md-3">
      <div :class="panelClass">
        <div class="panel-heading">
          <h3 class="panel-title">{{ title }}</h3>
        </div>
        <div class="panel-body">
          <Card v-for="(task, index) in tasks" @deleteTask="deleteTask" @moveLeft="moveLeft" @moveRight="moveRight" :task="task" :key="index" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Card from '@/components/Card'
  export default {
    props: ['title', 'tasks'],
    components: {
      Card
    },
    name: 'Panel',
    computed: {
      panelClass () {
        switch (this.title) {
          case 'ToDo': return 'panel panel-danger'
          case 'Doing': return 'panel panel-warning'
          case 'Review': return 'panel panel-primary'
          case 'Done': return 'panel panel-success'
        }
      }
    },
    methods: {
      deleteTask (task) {
        this.$emit('deleteTask', task);
      },
      moveLeft (task) {
        this.$emit('moveLeft', task);
      },
      moveRight (task) {
        this.$emit('moveRight', task);
      }
    }
  }
</script>

<style></style>