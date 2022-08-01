<template>
  <div id="app">
    <Axios></Axios>
    <hr>
    <Hello></Hello>
    <div style="height:150px"></div>
    <hr>
    <Interceptors></Interceptors>
    <hr>
    <Abort></Abort>
    <hr>
    <All></All>
  </div>
</template>

<script>
import Axios from './components/axios.vue'
import Hello from './components/hello.vue'
import Interceptors from './components/interceptors.vue'
import Abort from './components/abort.vue'
import All from './components/all.vue'
export default {
  name: 'App',
  components: {
    Axios,
    Hello,
    Interceptors,
    Abort, 
    All
  }
}
</script>

<style>
</style>
