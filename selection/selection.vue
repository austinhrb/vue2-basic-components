<template>
  <!-- selection div: -->
  <div class="selection-component">
    <!-- 当前选择要展示的内容：点击事件click(toggleDrop)进行切换 -->
    <div class="selection-show" @click="toggleDrop">
      <span>{{ selections[nowIndex].label }}</span>
      <!-- css3: arrow -->
      <div class="arrow"></div>
    </div>
    <!-- option: 隐藏显示isDrop-->
    <div class="selection-list" v-if="isDrop">
      <ul>
        <!-- 循环渲染li; 传入两个参数：index&item ;点击事件选中：chooseSelection-->
        <!-- 在v-for中声明index，在click的事件中传入 -->
        <li v-for="(item, index) in selections" @click="chooseSelection(index)">{{ item.label }}</li>
      </ul>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    props: {
      // selection 传入数组类型，默认给值test
      selections: {
        type: Array,
        default: [{
          label: 'test',
          value: 0
        }]
      }
    },
    data () {
      // selection: option的显现于隐藏isDrop; 当前选中项nowIndex
      return {
        isDrop: false,
        nowIndex: 0
      };
    },
    methods: {
      // 显示与隐藏的切换function
      toggleDrop () {
        this.isDrop = !this.isDrop;
      },
      // 点击切换事件
      chooseSelection (index) {
        this.nowIndex = index;   // 赋值
        this.isDrop = false;     // 显示
        this.$emit('on-change', this.selections[this.nowIndex]);
      }
    }
  };
</script>

<style scoped>
  .selection-component {
    position: relative;
    display: inline-block;
  }

  .selection-show {
    border: 1px solid #e3e3e3;
    padding: 0 20px 0 10px;
    display: inline-block;
    position: relative;
    cursor: pointer;
    height: 25px;
    line-height: 25px;
    border-radius: 3px;
    background: #fff;
  }

  .selection-show .arrow {
    display: inline-block;
    border-left: 4px solid transparent;
    border-right: 4px solid transparent;
    border-top: 5px solid #e3e3e3;
    width: 0;
    height: 0;
    margin-top: -1px;
    margin-left: 6px;
    margin-right: -14px;
    vertical-align: middle;
  }

  .selection-list {
    display: inline-block;
    position: absolute;
    left: 0;
    top: 25px;
    width: 100%;
    background: #fff;
    border-top: 1px solid #e3e3e3;
    border-bottom: 1px solid #e3e3e3;
    z-index: 5;
  }

  .selection-list li {
    padding: 5px 15px 5px 10px;
    border-left: 1px solid #e3e3e3;
    border-right: 1px solid #e3e3e3;
    cursor: pointer;
    background: #fff;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;

  }

  .selection-list li:hover {
    background: #e3e3e3;
  }
</style>
