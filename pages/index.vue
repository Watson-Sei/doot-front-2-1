<template>
  <div class="container">
    <div class="Side">Side</div>
    <div class="Content">
      <div class="chat">
        <div v-for="(item, index) in sendMessage" :key="index">
          <div v-if="item.user == `me`" class="mine messages">
            <div class="message last">
              {{ item.data }}
            </div>
            <span class="time">{{ item.time }}</span>
          </div>
          <div v-if="item.user == `other`" class="other messages">
            <div class="avatar">
              <font-awesome-icon icon = "user-circle" class="avatar-svg"/>
            </div>
            <div>
              <span class="user-name">経営者Aさん</span>
              <div class="message last">
                {{ item.data }}
              </div>
              <div class="time">
                {{ item.time }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
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
      if (this.message) {
        let date = new Date()
        this.sendMessage.push({user: 'me', data: this.message, time: date.toLocaleString()})
        this.BotChat(this.message)
        this.message = ''
      } else {
        alert("メッセージ未入力です。")
      }
    },
    BotChat(msg) {
      setTimeout(() => {
        let date = new Date()
        this.sendMessage.push({user: 'other', data: msg + "!!", time: date.toLocaleString()})
      }, 3000)
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
  background-color: #fff;
  overflow: auto;
  .chat {
    width: 100%;
    height: 100%;
    border: solid 1px #EEE;
    display: flex;
    flex-direction: column;
    padding: 40px;
    .messages {
      margin-top: 30px;
      display: flex;
      flex-direction: column;
      .message {
        border-radius: 20px;
        padding: 8px 15px;
        margin-top: 5px;
        margin-bottom: 5px;
        display: inline-block;
      }
      .time {
        font-size: 14px;
        color: gray;
      }
    }
    .other {
      align-items: flex-start;
      display: flex;
      flex-direction: row;
      .avatar {
        width: 40px;
        height: 40px;
        .avatar-svg {
          width: 70%;
          height: 70%;
        }
      }
      .user-name {
        font-size: 14px;
        color: gray;
      }
      .message {
        margin-right: 25%;
        background-color: #eee;
        position: relative;
      }
      .message.last::before {
        content: "";
        position: absolute;
        z-index: 0;
        bottom: 0;
        left: -7px;
        height: 20px;
        width: 20px;
        background: #eee;
        border-bottom-right-radius: 15px;
      }
      .message.last::after {
        content: "";
        position: absolute;
        z-index: 1;
        bottom: 0;
        left: -10px;
        width: 10px;
        height: 20px;
        background: white;
        border-bottom-right-radius: 10px;
      }
    }
    .mine {
      align-items: flex-end;
      .message {
        color: white;
        margin-left: 25%;
        background-color: #248bf5;
        background-attachment: fixed;
        position: relative;
      }
      .message.last:before {
        content: "";
        position: absolute;
        z-index: 0;
        bottom: 0;
        right: -8px;
        height: 20px;
        width: 20px;
        background-color: #248bf5;
        background-attachment: fixed;
        border-bottom-left-radius: 15px;
      }
      .message.last:after {
        content: "";
        position: absolute;
        z-index: 1;
        bottom: 0;
        right: -10px;
        width: 10px;
        height: 20px;
        background: white;
        border-bottom-left-radius: 10px;
      }
    }
  }
}


.Form {
  grid-row: 2 / 3;
  grid-column: 2 / 3;
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
