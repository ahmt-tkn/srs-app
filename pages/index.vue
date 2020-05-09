<template>
  <v-row>
    <v-col>
      <div v-if="$auth.loggedIn">
        <v-card class="mb-4">
          <v-app-bar dark color="blue">
            <v-toolbar-title>Dashboard Card</v-toolbar-title>
          </v-app-bar>

          <v-container>
            <v-row>
              <v-col>
                <v-list nav>
                  <v-list-item-group v-model="item" color="primary">
                    <v-list-item
                      v-for="item in items"
                      :key="item.id"
                      :to="`/${item.type}/${item.id}`"
                    >
                      <v-list-item-content>
                        <v-list-item-title
                          v-text="item.text"
                        ></v-list-item-title>
                      </v-list-item-content>
                    </v-list-item>
                  </v-list-item-group>
                </v-list>
              </v-col>
            </v-row>
          </v-container>
        </v-card>
      </div>
      <div v-else>Public Content</div>
    </v-col>
  </v-row>
</template>

<script>
/* import MainContent from '~/components/MainContent.vue' */

/* export default {
  components: {
    MainContent
  }
} */

export default {
  data: () => ({
    item: 1,
    items: [
      { text: 'ORG 1.1.1', type: 'r', id: 'WHEYWEASD' },
      { text: 'SXS-OMA', type: 'd', id: 'WEQDAWEASD' }
    ]
  }),
  middleware: 'auth',
  computed: {
    user() {
      return this.$auth.user
    }
  }
}
</script>
