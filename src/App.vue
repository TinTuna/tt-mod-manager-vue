<template>
  <v-app>
    <v-main>
      <ModManager/>
    </v-main>
  </v-app>
</template>

<script>
import ModManager from './components/ModManager';

export default {
  name: 'App',

  components: {
    ModManager,
  },

  data: () => ({
    //
  }),
};
</script>

<style scoped>
#app {
  background-color: black;
}
</style>