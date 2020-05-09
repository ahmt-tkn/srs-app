<template>
  <v-row dense>
    <v-col>
      <MainContent :content="content" />
    </v-col>
  </v-row>
</template>

<script>
import MainContent from '~/components/MainContent.vue'

export default {
  components: {
    MainContent
  },
  data() {
    return {
      content: {
        nodeID: this.$route.params.pathMatch.split('/')[1],
        nodeType: this.$route.params.pathMatch.split('/')[0]
      }
    }
  },
  head() {
    return {
      title: 'SRS - Question'
    }
  }
}
</script>
