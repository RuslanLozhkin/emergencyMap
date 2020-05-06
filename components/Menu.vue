<template>
  <v-navigation-drawer v-model="drawer" app clipped>
    <v-list dense>
      <v-list-item to="/" nuxt class="mt-10">
        <v-list-item-action>
          <v-icon>mdi-file-document-box</v-icon>
        </v-list-item-action>
        <v-list-item-content>
          <v-list-item-title>Главная</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
      <v-list-item to="/map" nuxt class="mt-4">
        <v-list-item-action>
          <v-icon>mdi-file-document-box</v-icon>
        </v-list-item-action>
        <v-list-item-content>
          <v-list-item-title>Карта</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
  </v-navigation-drawer>
</template>

<script>
export default {
  name: 'Menu',
  computed: {
    drawer: {
      get () {
        return this.$store.state.drawer
      },
      set (val) {
        this.$store.commit('drawer', val)
      }
    }
  }
}
</script>
