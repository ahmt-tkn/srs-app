<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :expand-on-hover="expandOnHover"
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
      <v-btn icon @click.stop="miniVariant = !miniVariant">
        <v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
      </v-btn>
      <v-btn icon @click.stop="clipped = !clipped">
        <v-icon>mdi-application</v-icon>
      </v-btn>
      <v-btn icon @click.stop="fixed = !fixed">
        <v-icon>mdi-minus</v-icon>
      </v-btn>
      <v-toolbar-title v-text="title" />
      <v-spacer />

      <h3>Hello, {{ $auth.loggedIn ? $auth.user.nickname : 'friend' }}!</h3>

      <v-btn v-if="$auth.loggedIn" to="/about" text small>Secret Button</v-btn>
      <v-btn v-if="$auth.loggedIn" text small @click="logout">Logout</v-btn>
      <v-btn v-else text small @click="login">Login</v-btn>

      <v-btn icon @click.stop="rightDrawer = !rightDrawer">
        <v-icon>mdi-menu</v-icon>
      </v-btn>
    </v-app-bar>
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
    <v-navigation-drawer v-model="rightDrawer" :right="right" temporary fixed>
      <v-list>
        <v-list-item @click.native="right = !right">
          <v-list-item-action>
            <v-icon light>
              mdi-repeat
            </v-icon>
          </v-list-item-action>
          <v-list-item-title>Switch drawer (click me)</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-footer :fixed="fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: true,
      drawer: true,
      fixed: false,
      expandOnHover: false,
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'SRS',
      items: [
        {
          icon: 'mdi-apps',
          title: 'Dashboard',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Regulations',
          to: '/regulations'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Documents',
          to: '/documents'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Login',
          to: '/auth/login'
        }
      ]
    }
  },
  methods: {
    login() {
      this.$auth.loginWith('auth0')
    },
    logout() {
      this.$auth.logout()
    }
  }
}
</script>
