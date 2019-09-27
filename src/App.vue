<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Robot</span>
        <span class="font-weight-light">Builder</span>
      </v-toolbar-title>
      <v-btn rounded color='primary' 
        text
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
      >
        <span class="mr-2">Latest Release</span>
      </v-btn>
    </v-app-bar>

    <v-content>
      <RobotBuilder/>
    </v-content>
  </v-app>
</template>

<script>
import RobotBuilder from './build/RobotBuilder.vue';
import { VApp, VAppBar, VToolbarTitle, VContent, VBtn } from 'vuetify/lib'

export default {
  name: 'App',
  components: {
    RobotBuilder,
    VApp,
    VAppBar,
    VToolbarTitle,
    VContent,
    VBtn
  },
  data: () => ({
    //
  }),
};
</script>
