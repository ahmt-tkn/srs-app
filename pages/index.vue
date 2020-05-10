<template>
  <v-container fluid>
    <v-row v-if="$auth.loggedIn">
      <v-col>
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
      </v-col>
    </v-row>
  </v-container>
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
      { text: 'SXS-MOE', type: 'd', id: 'WEQDAWEASD' }
    ]
  })
  /* ,
  computed: {
    user() {
      return this.$auth.user
    }
  } */
}
</script>
