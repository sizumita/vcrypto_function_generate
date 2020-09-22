<template>
  <v-container fluid>
    <Terms />
    <v-card>
      <v-card-title>実行内容</v-card-title>
    </v-card>
    <v-card>
      <v-card-title>出力テキスト</v-card-title>
    </v-card>
  </v-container>
</template>

<script>
import Terms from '@/components/terms/message_send.vue'

export default {
  comments: {
    Terms,
  },
  data() {
    return {
      terms: [{ type: 'user', lhs: '', symbol: '', rhs: '' }],
      content: [],
      selected: '',
      abc: '',
    }
  },
}
</script>
