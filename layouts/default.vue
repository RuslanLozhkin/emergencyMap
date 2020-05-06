<template>
  <v-app dark>
    <Menu />
    <Bar />
    <v-content>
      <nuxt />
    </v-content>
    <v-footer>
      <h3>
        &copy; 2020
      </h3>
      <v-spacer />
      <a href="#">
        <p>Github reposetory</p>
      </a>
    </v-footer>
  </v-app>
</template>

<script>

import Menu from '@/components/Menu'
import Bar from '@/components/Bar'

export default {
  components: {
    // eslint-disable-next-line vue/no-unused-components
    Menu,
    // eslint-disable-next-line vue/no-unused-components
    Bar
  },
  head () {
    return {
      title: 'Emergency Map software'
    }
  }
}
</script>

<style scoped>

</style>
