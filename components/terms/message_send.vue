<template>
  <v-card>
    <v-card-title>イベントの条件</v-card-title>
    <div class="text-center">
      <v-btn class="mx-2" fab small dark color="indigo" @click="terms.shift()">
        <v-icon dark>mdi-minus</v-icon>
      </v-btn>
    </div>
    <v-list v-model="terms">
      <v-list-item v-for="(term, i) in terms" :key="i">
        <v-container fluid>
          <v-row>
            <v-col cols="5">
              <v-combobox
                v-model="terms[i].lhs"
                :items="lhsList[term.type]"
                :label="lhsLabels[term.type]"
                outlined
                dense
                solo
              ></v-combobox>
            </v-col>
            <v-col cols="2">
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
            <v-col cols="5">
              <v-combobox
                v-model="terms[i].rhs"
                :items="rhsList[term.type]"
                :label="rhsLabels[term.type]"
                outlined
                dense
                solo
              ></v-combobox>
            </v-col>
          </v-row>
          <p>{{ value }}</p>
        </v-container>
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
}

const lhsLabels = {
  user: '対象ユーザー',
  channelName: '対象のチャンネル',
}

const symbols = {
  user: ['=='],
  channelName: ['==', '!=', 'in', 'starts', 'ends'],
}

const rhsList = {
  user: ['メッセージの送信者', 'サーバーオーナー', 'ランダムなユーザー'],
  channelName: [],
}

const rhsLabels = {
  user: 'ユーザーidもしくは選択',
  channelName: 'チャンネル名',
}

const types = [
  { name: 'ユーザーの種類', type: 'user' },
  { name: 'チャンネル名', type: 'channelName' },
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
