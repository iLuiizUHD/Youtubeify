<template>
  <v-app id="app">
    <v-app-bar app>
      <v-app-bar-nav-icon @click="drawer = true"> </v-app-bar-nav-icon>
      <v-toolbar-title> {{ $route.name }} </v-toolbar-title>

      <v-row class="ml-5 mr-5" style="margin-top: 15px">
        <v-col>
          <v-text-field
            v-model="query"
            label="Find songs"
            outlined
            dense
            @keypress.native.enter="findSongs"
          ></v-text-field>
        </v-col>
      </v-row>

      <v-btn icon @click="$vuetify.theme.dark = !$vuetify.theme.dark">
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn>
    </v-app-bar>

    <!-- Menu lateral -->
    <v-navigation-drawer v-model="drawer" temporary fixed>
      <v-list-item @click="drawer = !drawer">
        <v-list-item-icon>
          <v-icon>mdi-arrow-left</v-icon>
        </v-list-item-icon>
        <v-list-item-title>Close</v-list-item-title>
      </v-list-item>

      <v-list-item link to="/">
        <v-list-item-icon>
          <v-icon>mdi-home</v-icon>
        </v-list-item-icon>
        <v-list-item-title>Home</v-list-item-title>
      </v-list-item>

      <v-list-item link to="/playlists">
        <v-list-item-icon>
          <v-icon>mdi-format-list-bulleted</v-icon>
        </v-list-item-icon>
        <v-list-item-title>My playlists</v-list-item-title>
      </v-list-item>

      <v-divider></v-divider>

      <v-list dense nav style="position: fixed; bottom: 0; width: 100%">
        <v-list-item link to="/settings">
          <v-list-item-icon>
            <v-icon>mdi-cog</v-icon>
          </v-list-item-icon>
          <v-list-item-title>Settings</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-main app>
      <router-view app />
    </v-main>

    <player
      ref="$player"
      style="position: sticky; bottom: 0; width: 100%"
    ></player>
  </v-app>
</template>

<script>
import Player from "@/components/Player";

export default {
  name: "App",
  components: { Player },

  data: () => ({
    drawer: false,
    query: "",
  }),

  created() {
    this.$vuetify.theme.dark = true;
  },

  methods: {
    findSongs() {
      return this.$router.push(`/search?q=${this.query}`);
    },
  },
};
</script>

<style lang="scss">
@import "@/assets/scss/global.scss";
</style>
