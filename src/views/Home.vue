<template>
  <div id="home" class="d-flex flex-column align-items-center">
    <div id="startText" class="text-center rounded-circle my-5">完成很辛苦，<br>一步一步來也很辛苦；<br>若不做，永遠辛苦😄<br>開始吧！</div>
    <h1>{{ currentText }}</h1>
    <h2>{{ timetext }}</h2>
    <!-- icon 開始 -->
    <b-btn variant="primary" v-if="status !== 1" @click="start">
      GO
      <font-awesome-icon :icon="['fas','play']"></font-awesome-icon>
    </b-btn>
    <!-- icon 暫停 -->
    <b-btn variant="primary" v-if="status == 1" @click="pause">
      <font-awesome-icon :icon="['fas','pause']"></font-awesome-icon>
    </b-btn>
    <!-- icon 跳過 -->
    <b-btn variant="primary" v-if="current.length > 0 || todos.length > 0" @click="finish(true)">
      <font-awesome-icon :icon="['fas','step-forward']"></font-awesome-icon>
    </b-btn>
  </div>
</template>

<script>

export default {
  data () {
    return {
      // 0 = 停止
      // 1 = 播放
      // 2 = 暫停
      status: 0,
      timer: 0
    }
  },
  computed: {
    currentText () {
      // 清單中有東西 -> 就會出現'點擊開始'，如果沒東西 -> 就是'沒有事項'
      return this.current.length > 0 ? this.current : this.todos.length > 0 ? '點擊開始' : '沒有事項'
    },
    timetext () {
      // this.timeleft 在環境檔裡 為 5
      const m = Math.floor(this.timeleft / 60)
      const s = Math.floor(this.timeleft % 60)
      return `${m}：${s}`
    },
    alarm () {
      return this.$store.getters.alarm
    },
    timeleft () {
      return this.$store.getters.timeleft
    },
    current () {
      return this.$store.getters.current
    },
    todos () {
      return this.$store.getters.todos
    }
  },
  methods: {
    start () {
      // 暫停後繼續
      if (this.status === 2) {
        this.status = 1
        this.timer = setInterval(() => {
          this.$store.commit('countdown')
          if (this.timeleft <= 0) {
            this.finish(false)
          }
        }, 1000)
      } else {
      // 開始新倒數
        if (this.todos.length > 0) {
          this.$store.commit('start')
          this.status = 1
          this.timer = setInterval(() => {
            this.$store.commit('countdown')
            if (this.timeleft <= 0) {
              this.finish()
            }
          }, 1000)
        }
      }
    },
    finish (skip) {
      clearInterval(this.timer)
      this.status = 0
      this.$store.commit('finish')

      if (!skip) {
        const audio = new Audio()
        audio.src = './alarms/' + this.alarm
        audio.play()
      }

      if (this.todos.length > 0) {
        this.start()
      } else {
        alert('結束')
      }
    },
    pause () {
      clearInterval(this.timer)
      this.status = 2
    }
  }
}
</script>
