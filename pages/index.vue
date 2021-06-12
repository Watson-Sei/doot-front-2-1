<template>
  <div class="container">
    <div class="Side">Side</div>
    <div class="Content">Content</div>
    <div class="Form">Form</div>
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
  grid-template-columns: 350px 1fr;
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
}
</style>
