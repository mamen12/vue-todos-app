<template>
  <Header title="Task Tracker Todo"></Header>
  <FormInput/>

</template>

<script>
import Header from './components/Header.vue';
import  FormInput  from "./components/Forminput.vue";

export default {
  name: 'App',
  components: {
    Header,
    FormInput,
   
    
  }
}
</script>

<style scoped>

</style>