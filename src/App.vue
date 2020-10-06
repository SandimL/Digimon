<template>
  <v-app>
    <v-main>
      <!-- <HelloWorld/> -->
      <ListaDigimon/>
    </v-main>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld';
import ListaDigimon from './components/ListaDigimon';

export default {
  name: 'App',

  components: {
    // HelloWorld,
    ListaDigimon
  },

  data: () => ({
    //
  }),
};
</script>
