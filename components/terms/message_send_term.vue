<template>
  <v-card>
    <v-card-title>イベントの条件</v-card-title>
    <div class="text-center"></div>
    <v-list v-model="terms">
      <v-list-item v-for="(term, i) in terms" :key="i">
        <v-card color="blue-grey darken-3" class="mb-4">
          <h2 class="mt-2 ml-2">{{ term.name }}の条件</h2>
          <v-row class="ma-2">
            <v-col cols="12">
              <v-combobox
                v-model="terms[i].lhs"
                :items="lhsList[term.type]"
                :label="lhsLabels[term.type]"
                outlined
                dense
                solo
              ></v-combobox>
            </v-col>
            <v-col cols="12">
              <v-combobox
                v-model="terms[i].symbol"
                :items="symbols[term.type]"
                label="演算子"
                outlined
                class="text-center text-h5"
                dense
                solo
              ></v-combobox>
            </v-col>
            <v-col cols="12">
              <v-combobox
                v-model="terms[i].rhs"
                :items="rhsList[term.type]"
                :label="rhsLabels[term.type]"
                outlined
                dense
                solo
              ></v-combobox>
            </v-col>
            <v-col cols="12">
              <v-btn
                class="mx-2"
                fab
                small
                dark
                color="indigo"
                @click="terms = terms.filter((_, index) => index !== i)"
              >
                <v-icon dark>mdi-minus</v-icon>
              </v-btn>
            </v-col>
          </v-row>
        </v-card>
      </v-list-item>
    </v-list>
    <div class="text-center">
      <v-dialog v-model="dialog" width="500">
        <template v-slot:activator="{ on, attrs }">
          <v-btn
            class="mx-2"
            fab
            small
            dark
            color="indigo"
            v-bind="attrs"
            v-on="on"
          >
            <v-icon dark>mdi-plus</v-icon>
          </v-btn>
        </template>

        <v-card>
          <v-card-title class="headline" color="indigo">
            追加するイベントの条件を選択
          </v-card-title>
          <v-list v-model="types">
            <v-list-item v-for="(type, i2) in types" :key="i2">
              <v-btn
                @click="
                  terms.push({
                    type: type.type,
                    lhs: '',
                    rhs: '',
                    symbol: '',
                    name: type.name,
                  })
                  dialog = false
                "
                >{{ type.name }}
              </v-btn>
            </v-list-item>
          </v-list>

          <v-divider></v-divider>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="primary" text @click="dialog = false"> やめる </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </div>
  </v-card>
</template>

<script>
const lhsList = {
  user: ['メッセージの送信者', 'サーバーオーナー', 'ランダムなユーザー'],
  channelName: ['メッセージが送信されたチャンネル'],
  channel_id: ['メッセージが送信されたチャンネル'],
  message_id: ['イベントが発生するメッセージ'],
}

const lhsLabels = {
  user: '対象ユーザーを選択',
  channelName: '対象のチャンネルを選択',
  channel_id: '対象のチャンネルを選択',
  message_id: '対象のメッセージを選択',
}

const symbols = {
  user: ['=='],
  channelName: ['==', '!=', 'in', 'starts', 'ends'],
  channel_id: ['=='],
  message_id: ['=='],
}

const rhsList = {
  user: ['メッセージの送信者', 'サーバーオーナー', 'ランダムなユーザー'],
  channelName: [],
  channel_id: [],
  message_id: [],
}

const rhsLabels = {
  user: 'ユーザーidもしくは選択',
  channelName: 'チャンネル名を入力',
  channel_id: 'チャンネルidを入力',
  message_id: 'メッセージidを入力',
}

const types = [
  { name: 'ユーザーの種類', type: 'user' },
  { name: 'チャンネル名', type: 'channelName' },
  { name: 'チャンネルid', type: 'channel_id' },
  { name: 'メッセージid', type: 'message_id' },
]

export default {
  data() {
    return {
      lhsList,
      lhsLabels,
      symbols,
      rhsList,
      types,
      rhsLabels,
      dialog: false,
      terms: [],
    }
  },
}
</script>
