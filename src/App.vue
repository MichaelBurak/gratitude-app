<template>
  <v-app>
   
    <v-main>
      <!-- <HelloWorld/> -->
      <Header/>
      <GratefulList/>
      <Footer/>
    </v-main>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld';
import Header from './components/Header'
import GratefulList from './components/GratefulList'
import Footer from './components/Footer'
export default {
  name: 'App',

  components: {
    // HelloWorld,
    Header,
    GratefulList,
    Footer
  },

  data: () => ({
    //
  }),
};
</script>
