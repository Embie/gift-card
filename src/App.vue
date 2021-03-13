<template>
  <div id="app">
    <div class ="container">
      <div class="columns">
         <div class="column is-3"><grab-sidebar></grab-sidebar>
         </div>
         <div class="column is-6"><grab-form></grab-form>
         </div>
      </div>
    </div>
  </div>
</template>
<script>

import GrabForm from './components/GrabForm.vue'
import grabSidebar from './components/GrabSidebar.vue'
debugger
export default {
  name: 'App',
  components: { grabSidebar, GrabForm },
  data () {
    return {
      data: null
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: #f0f2f4;
}
</style>
