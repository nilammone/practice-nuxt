<template>
  <div>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />

      <!-- <v-toolbar-title v-text="title" /> -->

      <v-btn
        to="/"
        class="v-btn v-btn--text v-btn--tile theme--light v-size--default"
        ><span class="v-btn__content"> Home </span></v-btn
      >
      <v-btn
        to="/blog"
        class="v-btn v-btn--text v-btn--tile theme--light v-size--default"
        ><span class="v-btn__content"> Blog </span></v-btn
      >
      <v-btn
        to="/profile"
        class="v-btn v-btn--text v-btn--tile theme--light v-size--default"
        ><span class="v-btn__content"> Profile </span></v-btn
      >

      <v-menu>
        <template #activator="{ on, attrs }">
          <v-btn dark v-bind="attrs" v-on="on"> More </v-btn>
        </template>
        <v-list>
          <v-list-item v-for="(menuitem, index) in menuitems" :key="index">
            <v-list-item-title>
              <v-btn
                :to="menuitem.link"
                class="v-btn v-btn--text v-btn--tile theme--light v-size--default"
                ><span class="v-btn__content">
                  {{ menuitem.title }}
                </span></v-btn
              >
            </v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>

      <v-spacer />
      <v-btn v-if="loggedIn" color="error" @click="logout">Log Out</v-btn>
      <v-btn v-else to="/login" color="success">Log In</v-btn>
    </v-app-bar>
  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire',
        },
      ],
      menuitems: [
        { title: 'About', link: '/about' },
        { title: 'Photos', link: 'photos' },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js',
    }
  },
  computed: {
    ...mapState('auth', ['loggedIn']),
  },
  methods: {
    async logout() {
      await this.$auth.logout()

      this.$router.push('/login')
    },
  },
}
</script>

<style scoped></style>
