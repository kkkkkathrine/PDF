<template>
  <div class="root-container">
    <div class="container">
      <div class="top-section">
        <div class="knowledge-candidates" style="display: flex; width: 100%">
          <!-- 循环渲染知识候选项 -->
          <div
            v-for="candidate in knowledgeCandidates"
            :key="candidate.id"
            class="candidate-item"
            style="flex: 1"
          >
            <div class="candidate-info">
              <div style="margin-right: 20px">{{ candidate.title }}</div>
              <div>
                <p v-for="(candidate, idx) in candidate.content.split(',')" :key="idx">
                  <label for=""> <input type="checkbox" :name="idx" /> {{ candidate }} </label>
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="bottom-section">
        <div class="relation-slider">
          <div class="relation-container">
            <!-- 循环渲染超关系 -->
            <div class="relation-item-row">
              <div class="relation-item" style="height: 50vh;min-height:500px width: 100%">
                <jsMind refid="mind1" v-if="Library" :mind="mind1"></jsMind>
              </div>
              <div class="relation-item" style="height: 50vh; min-height: 500px; width: 100%">
                <jsMind refid="mind2" v-if="Library" :mind="mind2"></jsMind>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="button-group">
        <!-- 确认知识库按钮 -->
        <button class="confirm-library-btn" @click="confirmLibrary">确认知识库</button>
        <!-- 超关系确认按钮 -->
        <button class="confirm-relation-btn" @click="confirmRelation">超关系确认</button>
      </div>
    </div>
    <Tip ref="tip"></Tip>
  </div>
</template>

<script>
import jsMind from "./components/JsMind";
import Tip from "./components/Tip";

export default {
  data() {
    return {
      knowledgeCandidates: [
        // 知识候选项数据
        { id: 1, title: "entity:", content: "CDE,药品化学名,治疗,高血压", waiting: false },
        { id: 2, title: "relation:", content: "CDE,药品化学名,治疗,高血压", waiting: false },
        { id: 3, title: "key:", content: "CDE,药品化学名,治疗,高血压", waiting: false },
        { id: 4, title: "value:", content: "CDE,药品化学名,治疗,高血压", waiting: false },
      ],

      Library: false,
      Relation: false,
      mind1: {
        meta: {
          name: "治疗",
        },
        format: "node_tree",
        data: {
          id: "root",
          topic: "治疗",
          children: [
            {
              id: "CDE",
              topic: "CDE",
              direction: "right",
              children: [],
            },
            {
              id: "open",
              topic: "高血压",
              direction: "right",
              children: [],
            },
            {
              id: "KV",
              topic: "KV",
              direction: "right",
              children: [
                { id: "open1", topic: "适应症 奸娠高高血压急症" },
                { id: "open2", topic: "适应症 高血压急症" },
              ],
            },
          ],
        },
      },
      mind2: {
        meta: {
          name: "治疗",
        },
        format: "node_tree",
        data: {
          id: "root1",
          topic: "治疗",
          children: [
            {
              id: "应用他汀类药物1",
              topic: "应用他汀类药物",
              direction: "right",
              children: [],
            },
            {
              id: "open1",
              topic: "高血压",
              direction: "right",
              children: [],
            },
            {
              id: "KV1",
              topic: "KV",
              direction: "right",
              children: [
                { id: "open11", topic: "高血压合并临床疾病 是" },
                { id: "open21", topic: "应用他汀类作为心血管疾病的一级预防 是" },
                { id: "open31", topic: "应用他汀类作为心血管疾病的二级预防 是" },
              ],
            },
          ],
        },
      },
    };
  },
  components: {
    jsMind,
    Tip,
  },
  mounted() {},

  methods: {
    confirmLibrary() {
      this.Library = true;
    },
    confirmRelation() {
      this.$refs.tip.open();
    },
  },
};
</script>

<style>
.modelTest .sidebox-backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 199;
  background-color: rgb(31 33 38 / 25%);
}

/* * {
  padding: 0;
  margin: 0;
} */
.container {
  display: flex;
  flex-direction: column;
  height: 100vh;
  background-color: #f6fcfe;
}

.top-section {
  flex: 1;
  background-color: #e4effe;
  display: flex;
  align-items: center;
  justify-content: center;
  height: calc(100vh / 3);
  /* 上半部分高度占1/3 */
  overflow: hidden;
  /* 取消滚动条 */
}

.knowledge-candidates {
  display: flex;
  justify-content: space-between;
  /* 知识库水平均匀分布 */
  height: 100%;
  /* 使知识库占满上半部分高度 */
  padding: 10px;
  /* 添加间距 */
  font-size: 30px;
  /* 调整知识库文字大小 */
  text-align: center;
  /* 居中显示 */
}

.candidate-item {
  flex: 1;
  text-align: center;
  border: 3px solid #53b5df;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 20px;
  /* 添加间距 */
  font-weight: bold;
  /* 标题样式 */
}
.candidate-info {
  display: flex;
}

.candidate-info p {
  font-weight: normal;
  text-align: left;
  width: 200px;
  margin: 0;
}

.bottom-section {
  position: relative;
  display: flex;
  align-items: flex-end;
}

.relation-slider {
  width: 100%;
  max-height: 100%;
  /* 超关系占据上半部分的2/3高度 */
  overflow: auto;
}

.relation-container {
  padding: 10px;
  position: relative;
}

.relation-item-row {
  display: flex;
  justify-content: space-between;
  /* 超关系水平均匀分布 */
  margin-bottom: 10px;
}

.relation-item {
  flex: 1;
  text-align: center;
  /* padding: 55px; */
  min-height: 120px;

  border: 3px solid #6aa0b4;
  margin-right: 5px;
  /* 添加间距 */
  font-weight: bold;
  /* 标题样式 */
}

.relation-info {
  /* 添加超关系信息样式 */
}

.button-group {
  display: flex;
  justify-content: flex-end;
  padding: 0px;
  /* margin-top: 10px; */
  padding-bottom: 10px;
  /* 添加上边距，与内容分隔开 */
}

.confirm-library-btn,
.confirm-relation-btn {
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
  /* 添加这一行以防止按钮中的文字换行 */
}

.confirm-library-btn:hover,
.confirm-relation-btn:hover {
  background-color: #428fad;
}
</style>
