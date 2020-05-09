<template>
  <v-card class="pa-2">
    <v-app-bar dark color="green">
      <v-toolbar-title>Regulation</v-toolbar-title>
    </v-app-bar>

    <v-container>
      <v-row>
        <v-col cols="12">
          Content
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
export default {
  data: () => ({
    cards: [
      {
        title: 'Pre-fab homes',
        src: 'https://cdn.vuetifyjs.com/images/cards/house.jpg',
        flex: 12
      },
      {
        title: 'Favorite road trips',
        src: 'https://cdn.vuetifyjs.com/images/cards/road.jpg',
        flex: 6
      },
      {
        title: 'Best airlines',
        src: 'https://cdn.vuetifyjs.com/images/cards/plane.jpg',
        flex: 6
      }
    ]
  })
}
</script>
