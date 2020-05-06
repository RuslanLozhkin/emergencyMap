<template>
  <v-app-bar app clipped-left>
    <v-app-bar-nav-icon @click.stop="toggleDrawer" />
    <v-toolbar-title>Emergency Map Dashboard</v-toolbar-title>
    <v-spacer />
    <v-btn icon @click="handleFullScreen()">
      <v-icon>mdi-fullscreen</v-icon>
    </v-btn>
    <v-menu
      offset-y
      origin="center center"
      :nudge-right="140"
      :nudge-bottom="10"
      transition="slide-y-transition"
    >
      <template v-slot:activator="{ on }">
        <v-btn icon large text v-on="on">
          <v-avatar size="30px">
            <v-icon>mdi-account</v-icon>
          </v-avatar>
        </v-btn>
      </template>
      <v-list class="pa-0">
        <v-list-item href="/about" ripple="ripple" rel="noopener">
          <v-list-item-action>
            <v-icon>mdi-information-variant</v-icon>
          </v-list-item-action>

          <v-list-item-content>
            <v-list-item-title>About...</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item href="#" ripple="ripple" rel="noopener" @click="$auth.logout()">
          <v-list-item-action>
            <v-icon>mdi-logout</v-icon>
          </v-list-item-action>

          <v-list-item-content>
            <v-list-item-title>Выход</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-menu>
  </v-app-bar>
</template>
<script>
import Util from '@/util'
export default {
  name: 'Bar',
  methods: {
    toggleDrawer () {
      this.$store.commit('toggleDrawer')
    },
    handleFullScreen () {
      Util.toggleFullScreen()
    }
  }
}
</script>
