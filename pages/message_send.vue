<template>
  <v-container fluid>
    <MessageSendTerm />
    <v-card>
      <v-card-title>実行内容</v-card-title>
    </v-card>
    <v-card>
      <v-card-title>出力テキスト</v-card-title>
    </v-card>
  </v-container>
</template>

<script>
import MessageSendTerm from '@/components/terms/message_send_term.vue'

export default {
  comments: {
    MessageSendTerm,
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
