<template>
  <v-app>
    <Home/>
  </v-app>
</template>

<script>
import Vue from 'vue'
import Home from './views/Home';
import axios from 'axios'
import VueAxios from 'vue-axios'
 
Vue.use(VueAxios, axios)

export default {
  name: 'App',

  components: {
    Home,
  },

  data: () => ({
    //
  }),
};
</script>
