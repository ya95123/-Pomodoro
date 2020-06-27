<template>
  <div id="settings">
    <h3>鈴 聲 設 定</h3>
    <b-table :items="items" :fields="fields" @row-clicked="selectAlarm">
      <template v-slot:cell(preview)="data">
        <!-- why 是 item 不是 items ? -->
        <audio controls width="100" :src="'./alarms/'+data.item.file"></audio>
      </template>

      <template v-slot:cell(select)="data">
        <!-- data.item.file == alarm | alarm 為 store 的 getters 傳遞過來的 function -->
        <font-awesome-icon v-if="data.item.file == alarm" :icon="['fas','check']"></font-awesome-icon>
      </template>
    </b-table>
  </div>
</template>

<script>
export default {
  data () {
    return {
      items: [
        {
          name: '鬧鈴',
          file: 'alarm1.mp3'
        },
        {
          name: '風鈴',
          file: 'alarm2.mp3'
        },
        {
          name: '歡呼',
          file: 'yay.mp3'
        }
      ],
      fields: [
        {
          key: 'name',
          label: '名稱'
        },
        {
          key: 'preview',
          label: '試聽'
        },
        {
          key: 'select',
          label: '選擇'
        }
      ]
    }
  },
  computed: {
    alarm () {
      return this.$store.getters.alarm
    }
  },
  methods: {
    selectAlarm (item) {
      // 傳進 store
      this.$store.commit('selectAlarm', item.file)
    }
  }
}

</script>
