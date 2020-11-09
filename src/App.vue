<template>
  <v-app>
   
    <v-main>
      <!-- <HelloWorld/> -->
      <Header/>
      <GratefulList/>
    </v-main>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld';
import Header from './components/Header'
import GratefulList from './components/GratefulList'

export default {
  name: 'App',

  components: {
    // HelloWorld,
    Header,
    GratefulList
  },

  data: () => ({
    //
  }),
};
</script>
