<template>
  <v-app id="srs-app">
    <v-navigation-drawer
      v-if="$auth.loggedIn"
      v-model="drawerRight"
      app
      clipped
      right
      temporary
    >
      <v-list>
        <v-list-item two-line>
          <v-list-item-avatar>
            <img :src="$auth.loggedIn ? $auth.user.picture : ''" />
          </v-list-item-avatar>

          <v-list-item-content>
            <v-list-item-title>{{
              $auth.loggedIn ? $auth.user.nickname : 'Nickname'
            }}</v-list-item-title>
            <v-list-item-subtitle>{{
              $auth.loggedIn ? $auth.user.email : 'Email'
            }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <v-divider></v-divider>
      <v-list nav dense>
        <v-list-item-group v-model="item" color="primary">
          <v-list-item v-for="(item, i) in items" :key="i" :to="item.to">
            <v-list-item-icon>
              <v-icon v-text="item.icon"></v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title v-text="item.text"></v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
      <v-divider></v-divider>
      <v-list nav dense>
        <v-list-item @click="logout">
          <v-list-item-action>
            <v-icon>mdi-logout</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Sign out</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app clipped-right color="primary" dark>
      <v-toolbar-title style="width: 200px" class="ml-0 pl-4">
        <span class="hidden-sm-and-down">{{ title }}</span>
      </v-toolbar-title>
      <v-spacer />
      <v-text-field
        v-if="$auth.loggedIn"
        flat
        solo-inverted
        hide-details
        prepend-inner-icon="mdi-magnify"
        label="Search"
        class="hidden-sm-and-down"
      ></v-text-field>
      <v-spacer />
      <v-btn
        v-if="$auth.loggedIn"
        icon
        @click.stop="drawerNotification = !drawerNotification"
      >
        <v-icon>mdi-bell</v-icon>
      </v-btn>
      <v-btn
        v-if="$auth.loggedIn"
        icon
        @click.stop="drawerRight = !drawerRight"
      >
        <v-icon>mdi-account</v-icon>
      </v-btn>
      <v-btn v-if="$auth.loggedIn" icon @click="logout">
        <v-icon>mdi-logout</v-icon>
      </v-btn>
      <v-btn v-if="!$auth.loggedIn" icon @click="login">
        <v-icon>mdi-login</v-icon>
      </v-btn>
    </v-app-bar>

    <v-content>
      <nuxt v-if="$auth.loggedIn" />
      <v-container v-else fluid class="fill-height">
        <v-row justify="center" align="center">
          <v-col class="shrink">
            <v-tooltip right>
              <template v-slot:activator="{ on }">
                <v-btn :href="source" icon large target="_blank" v-on="on">
                  <v-icon large>mdi-code-tags</v-icon>
                </v-btn>
              </template>
              <span>Source</span>
            </v-tooltip>
          </v-col>
        </v-row>
      </v-container>
    </v-content>

    <v-navigation-drawer
      v-if="$auth.loggedIn"
      v-model="drawerNotification"
      app
      clipped
      right
      temporary
    >
      Notification
    </v-navigation-drawer>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawerRight: false,
    drawerNotification: false,
    title: 'SRS',
    item: 0,
    items: [
      { text: 'Dashboard', icon: 'mdi-view-dashboard-outline', to: '/' },
      { text: 'Regulations', icon: 'mdi-text-box', to: 'regulations' },
      { text: 'Documents', icon: 'mdi-file-document-outline', to: 'documents' }
    ]
  }),
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
