<template>
  <div class="searchArea">
    <!--左边现实历史查询记录-->
    <div class="panel">
      <div class="memoBox"><a href=" ">2023.9.23</a></div>
      <div class="memoBox"><a href=" ">2023.9.23</a></div>
      <div class="memoBox"><a href=" ">2023.9.23</a></div>
    </div>
    <!--右边显示查询界面-->
    <div class="background">
      <div class="messageContainer">
        <div class="greetings">
          <div class="messageBlock">Hi! Feel free to talk to me!</div>
        </div>
        <div  class="userMassage">
          <div v-for="message in messages" :key="message.id" class="messageBlock">{{ message.text }}</div>
        </div>
      </div>
      <div>
        <form @submit.prevent="sendMessage" class="inputArea">
        <textarea
          v-model="inputText"
          type="textarea"
          placeholder="Input your words..."
        ></textarea>
          <button type="submit">send</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputText: '',
      messages: [],
    };
  },
  methods: {
    sendMessage() {
      if (this.inputText.trim()) {
        this.messages.push({ id: Date.now(), text: this.inputText});
        this.inputText = '';
      }
    },
  }
}
</script>

<style scoped>
.searchArea{
  display: flex;
  height: 80vh;
  flex-direction: row;
}
.searchArea .panel{
  width: 250px;
  background-color: rgb(0, 21, 41);
  flex-direction: column;
  justify-content: center;
  overflow-x: hidden;
  overflow-y: auto;
}
.memoBox{
  margin: 10px;
  background-color: #1677ff;
  color: white;
  border-radius: 8px;
  padding: 10px;
  cursor: pointer;
}
a:link{color: white}
a:visited{color: white}
a:hover{font-size: 120%}
.background{
  display: flex;
  flex-direction: column;
  flex: 1;
  background: linear-gradient(to bottom right,#dbe6fb, #f3f4f8);
  background-size: cover;
  background-attachment: fixed;
}
.messageContainer{
  flex: 1;
  width: 100%;
  max-width: 1000px;
  margin: 0 auto;
  flex-direction: column;
  overflow-y: auto;
}
.greetings{
  float: left;
}
.userMassage{
  float: right;
  flex-direction: column;
}
.messageBlock {
  margin: 10px 10px;
  border-radius: 8px;
  padding: 6px 12px;
  max-width: 800px;
  background: rgba(255, 255, 255, 0.6);
  font-size: 14px;
  box-shadow:  0px 0.3px 0.9px rgba(0, 0, 0, 0.12), 0px 1.6px 3.6px rgba(0, 0, 0, 0.16);
}
.userMassage .messageBlock{
  background: linear-gradient(90deg, #2870EA 10.79%, #1B4AEF 87.08%);;
  color: #fff;
}
.inputArea{
  display: flex;
  padding: 5px 10px;
  max-width: 1000px;
  margin: 0 auto;
  width: 100%;
}
.inputArea textarea{
  flex: 1;
  border-color: #d9d9d9;
  resize: none;
  outline: none;
  padding: 0px 5px;
  height: 35px;
  line-height: 30px;
  color: #404040;
  border-radius: 10px 0px 0px 10px;
  transition: all 0.3s,height 0s;
}
.inputArea textarea:hover{
  border-color: #4096ff;
}
.inputArea button{
  height: 35px;
  color: #fff;
  background: linear-gradient(90deg, #2870EA 10.79%, #1B4AEF 87.08%);
  box-shadow: 0 2px 0 rgba(5, 145, 255, 0.1);
  border: none;
  padding: 0 20px;
  border-radius: 0px 8px 8px 0px;
  cursor: pointer;
}
.inputArea button:hover{
  background-color: #388aff;
}
</style>
