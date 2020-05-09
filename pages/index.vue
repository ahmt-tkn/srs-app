<template>
  <v-row>
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
                      <v-list-item-title v-text="item.text"></v-list-item-title>
                    </v-list-item-content>
                  </v-list-item>
                </v-list-item-group>
              </v-list>
            </v-col>
          </v-row>
        </v-container>
      </v-card>
      <v-card class="mb-4">
        <v-app-bar dark color="blue">
          <v-toolbar-title>Dashboard Card</v-toolbar-title>
        </v-app-bar>

        <v-container>
          <v-row>
            <v-col>
              <super-secret-div v-if="$auth.loggedIn" />
            </v-col>
          </v-row>
        </v-container>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import SuperSecretDiv from '~/components/SuperSecretDiv'
/* import MainContent from '~/components/MainContent.vue' */
/* import RelatedRegulations from '~/components/RelatedRegulations.vue'
import RelatedDocuments from '~/components/RelatedDocuments.vue' */

/* export default {
  components: {
    MainContent
  }
} */
export default {
  components: {
    SuperSecretDiv
  },
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
