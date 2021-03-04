<template>
  <!-- App.vue -->

  <v-app>
    <v-navigation-drawer
      :height="dynamicDrawerHeight"
      temporary
      right
      bottom
      app
      v-model="showNavigationDrawer"
    >
      <template slot="prepend">
        <div
          id="draggableNotch"
          class="d-flex justify-center"
          @dragover="resetResizing"
          @drag="increaseHeight"
        >
          botão arrastar
        </div>
      </template>
      <!-- -->
    </v-navigation-drawer>
    <v-system-bar color="red" app height="80px"></v-system-bar>
    <v-app-bar app>
      <h1 @click.stop="showNavigationDrawer = !showNavigationDrawer">carrega</h1>
      <!-- -->
    </v-app-bar>

    <!-- Sizes your content based upon application components -->
    <v-main>
      <!-- Provides the application the proper gutter -->
      <v-container fluid>
        <!-- If using vue-router -->
        <router-view></router-view>
      </v-container>
    </v-main>

    <v-footer app>
      <!-- -->
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    showNavigationDrawer: true,
    group: null,
    drawerHeight: "30%",
    reziseDrawer: true,
  }),
  computed: {
    dynamicDrawerHeight: function () {
      if (this.reziseDrawer) {
        return this.drawerHeight;
      } else {
        return Math.floor(window.innerHeight * 0.3) + "px";
      }
    },
  },

  watch: {
    group() {
      this.drawer = false;
    },
  },
  methods: {
    increaseHeight: function (event) {
      event.preventDefault();
      console.log(event);
      this.reziseDrawer = true;
      console.log(event.clientY);
      console.log(window.innerHeight);

      this.drawerHeight = window.innerHeight - event.clientY;
      console.log("joao");
    },
    resetResizing: function (event) {
      event.preventDefault();
      console.log(event.clientY);
      console.log(window.innerHeight);
      console.log("largar");
    },
  },
};
</script>

<style lang="scss" scoped>
.v-navigation-drawer--bottom.v-navigation-drawer--is-mobile {
  max-height: 90%;
}
</style>
