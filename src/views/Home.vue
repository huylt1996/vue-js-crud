<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <CRUD msg="Hello Program"/> <!--:list-person ="listPerson"-->
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import CRUD from '@/components/crud.vue';
/* eslint-disable */
export default {
  name: 'Home',
  components: {
    HelloWorld,
    CRUD
  }
  // ,
  // data() {
  //    return {
  //      listPerson:  [
  //       {stt: 1, firstName: 'Huy', lastName: 'Lee'},
  //       {stt: 2, firstName: 'Dao', lastName: 'Lee'}
  //     ]
  // }
  // }
  // ,
  // methods: {
  //   onUpdate(data) {
  //     debugger;
  //     this.listPerson = data;
  //     console.log(data);
  //   }
  // }
}
</script>
