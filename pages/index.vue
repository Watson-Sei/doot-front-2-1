<template>
  <div class="container">
    <div class="Side">Side</div>
    <div class="Content">Content</div>
    <div class="Form">
      <div class="form-content">
        <input v-model="message" placeholder="ENTERキーで送信(上限800文字)" maxlength="800" />
        <button @click="sendChat">送信</button>
      </div>
    </div>
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
.container {
  display: grid;
  height: 100vh;
  grid-template-rows: 1fr 100px;
  grid-template-columns: 300px 1fr;
}
.Side {
  grid-row: 1 / 3;
  grid-column: 1 / 2;
  background: #f88;
}
.Content {
  grid-row: 1 / 2;
  grid-column: 2 / 3;
  background: #8f8;
}
.Form {
  grid-row: 2 / 3;
  grid-column: 2 / 3;
  background: #88f;
  display: table;
  width: 100%;
}
.form-content {
  display: table-cell;
  vertical-align: middle;
  text-align: center;
}
.form-content input {
  width: 70%;
  height: 40px;
}
.form-content button {
  height: 40px;
}
</style>
