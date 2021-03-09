<template>
  <v-app>
    <v-app-bar
      app
      color="warning"
      dark
    >
      <div class="d-flex align-center">
      <v-icon>mdi-48px mdi-magnify</v-icon>

      <h1>Search App</h1>
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2"></span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <Search_page/>
    </v-main>
  </v-app>
</template>

<script>
import Search_page from './components/Search_page';

export default {
  name: 'App',

  components: {
    Search_page,
  },

  data: () => ({
    //
  }),
};
</script>
