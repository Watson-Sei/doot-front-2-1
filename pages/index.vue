<template>
  <div>
    <p>データ:</p>
    <p>{{ sendMessage }}</p>
    <input v-model="message"/>
    <button @click="sendChat">送信</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: '',
      sendMessage: [],
    }
  },
  methods: {
    sendChat() {
      this.sendMessage.push({user: 'me', data: this.message})
      this.BotChat(this.message)
      this.message = ''
    },
    BotChat(msg) {
      this.sendMessage.push({user: 'other', data: msg + "!!"})
    }
  }
}
</script>

<style lang="scss" scoped>
.split{
  display: table;
  width: 100%;
}
.split-item {
  display: table-cell;
  padding: 80px;
  width: 50%;
}
.split-left {
  background: #000;
  color: #fff;
  position: relative;
}
.split-left__inner {
  height: 100%;
  position: fixed;
  width: 50%;
}
.split-right__inner {
  height: 8000px;
}
</style>
