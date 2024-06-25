<template>
  <v-app>
    <v-main>
      <v-app-bar>
        <v-app-ver-title>
          学マス計算機
        </v-app-ver-title>
      </v-app-bar>
      <TurnComponent/>
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import TurnComponent from './components/TurnComponent.vue';

export default {
  name: 'App',

  components: {
    HelloWorld,
    TurnComponent,
  },

  data: () => ({
    //
  }),
}
</script>
