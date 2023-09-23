<template>
  <!-- 绑定isShow，是否显示，同时绑定点击事件，相当点击空白区域 -->
  <div class="app" v-if="isShow" @click="blank">
    <div class="card">
      <div class="text">
        "data": [
        {'header':'CDE','headerType':'药品化学名','relation':'治疗','tailer':'高血压','tailerType':'疾病','KV':[{'key':'适应症',
        'value':'妊娠高高血压急症', 'valueType':'疾病' },{ 'key':'适应症', 'value':'高血压急症',
        'valueType':'疾病' }]},{ 'header': '应用他汀类药物', 'headerType': '治疗', 'tailer':
        '高血压', 'tailerType': '疾病', 'KV': [ { 'key': '合并≥1种代谢性危险因素', 'value': '是',
        'valueType': '疾病' }, { 'key': '伴靶器官损害', 'value':'是', 'valueType': '疾病' }, {
        'key': '高血压合并临床疾病', 'value': '是', 'valueType': '疾病' }, { 'key':
        '应用他汀类作为心血管疾病的一级预防', 'value': '是', 'valueType': '治疗' }, { 'key':
        '应用他汀类作为心血管疾病二级预防', 'value': '是', 'valueType': '治疗' } ]} ]
      </div>
      <br />
      <div class="btn">
        <button @click="cancel">取消</button>
        <button @click="confirm" class="confirm">确认</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SpringFrame",
  props: {
    title: {
      type: String,
      default: "标题",
    },
  },
  data() {
    return {
      isShow: false,
    };
  },
  computed: {},
  methods: {
    //点击确认时通过$emit传递事件过去
    cancel() {
      this.isShow = false;

      this.$emit("cancel");
    },
    open() {
      this.isShow = true;
    },
    confirm() {
      this.isShow = false;
      //点击取消时通过$emit传递事件过去
      this.$emit("confirm");
    },
    //点击空白区域相当于点击取消事件
    blank(e) {
      /* 看点击的节点是不是最外层 */
      if (e.target.className == "app") {
        this.cancel();
      }
    },
  },
  watch: {},
  created() {},
  mounted() {},
};
</script>
<style scoped>
.app {
  position: fixed;
  inset: 0;
  z-index: 10000;
  background-color: rgba(194, 194, 194, 0.2);
}
.card {
  position: absolute;
  top: 50%;
  left: 50%;
  min-width: 250px;
  transform: translate(-50%, -50%);
  box-shadow: 0 0 8px rgb(219, 219, 219);
  background-color: #fff;
  padding: 10px 15px;
}
.card > h2 {
  text-align: center;
  font-size: 20px;
  line-height: 25px;
  
}
.text {
  min-height: 100px;
  max-height: 70vh;
  max-width: 600px;
  padding: 20px;
  overflow: auto;
}
.btn > button {
  padding: 5px;
  margin-left: 5px;
  float: right;
  text-align: center;
  font-family: "fangsong";
  font-weight: bold;
  font-size: 18px;
  border: none;
  box-shadow: -2px -2px 8px -2px white, 2px 2px 8px -2px rgba(0, 0, 0, 0.15);
  border-radius: 5px;
  cursor: pointer;
}
button:active {
  box-shadow: inset -2px -2px 8px -2px white, inset 2px 2px 8px -2px rgba(0, 0, 0, 0.15);
}
.confirm {
  background-color: #53b5df;
  color: white;
  border: 0px solid;
  padding: 5px 10px;
  border-radius: 10px;
  font-size: 15px;
  cursor: pointer;
  transition: background-color 0.3s ease-in-out;
  margin: 0 10px;
  /* 添加按钮之间的水平间距 */
  white-space: nowrap;
  color: #fff;

}
</style>
