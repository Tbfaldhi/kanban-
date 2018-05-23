<template>
  <div class="home">
    <Board></Board>
    <Panel></Panel>
  </div>
</template>

<script>
// @ is an alias to /src

import Board from '@/components/Board.vue'
import Panel from '@/components/Panel.vue'

export default {
  name: 'home',
  components: {
  Board,
  Panel
  }
}
</script>
