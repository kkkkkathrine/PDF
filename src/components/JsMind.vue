<template>
  <!-- 显示思维导图容器 -->
  <div :ref="refid" style="width: 100%; height: 100%"></div>
</template>

<script>
import "jsmind/style/jsmind.css";
import jsMind from "jsmind";

export default {
  name: "MindMap",
  props: {
    refid: { type: String, required: true }, // 组件的引用 ID，必需属性
    mind: { type: Object, required: true }, // 传递的思维导图数据，必需属性
  },
  data() {
    return {
      mindMap: null, // 存储 jsMind 实例
      history: [],   // 存储历史状态，用于撤销操作
      current: -1,   // 记录当前历史状态的索引
    };
  },
  mounted() {
    // jsMind 配置选项
    const options = {
      container: this.$refs[this.refid], // 使用 refid 引用的容器
      view: {
        engine: "canvas",                 // 使用 canvas 引擎
        hmargin: 20,                      // 水平边距
        vmargin: 20,                      // 垂直边距
        draggable: true,                  // 节点是否可拖动
        hide_scrollbars_when_draggable: true, // 拖动节点时隐藏滚动条
      },
    };
    // 创建 jsMind 实例并显示思维导图
    this.mindMap = new jsMind(options);
    this.mindMap.show(this.mind);
  },
};
</script>

<style>
.jmnode-overflow-hidden {
  display: flex;
  justify-content: center; /* 水平居中对齐 */
  /* align-items: center; */ /* 垂直居中对齐（已注释掉） */
}
</style>
