<template>
  <v-card class="mb-4">
    <v-app-bar dark color="blue">
      <v-toolbar-title>Main Content - Type: {{ nodeType }}</v-toolbar-title>
    </v-app-bar>

    <v-container>
      <v-row>
        <v-col>
          {{ nodeID }}
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
export default {
  props: {
    content: {
      type: Object,
      default: null
    }
  },
  data() {
    return {
      nodeID: this.content.nodeID,
      nodeType: this.content.nodeType
    }
  }
}
</script>
