<!--
选项卡:多选
与单选类似，只是处理函数的不一样：在methods方法里面的处理

-->
<template>
  <div>
    <div class="chooser-component">
      <ul class="chooser-list">
        <li v-for="(item, index) in selections"
            @click="toggleSelection(index)"
            :title="item.label"
            :class="{active: checkActive(index)}"
        >{{ item.label }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import _ from 'lodash';
  // lodash 语法
  export default {
    props: {
      selections: {
        type: Array,
        default: [{
          label: 'test',
          value: 0
        }]
      }
    },
    data () {
      return {
        nowIndexes: [0]
      };
    },
    methods: {
      toggleSection (index) {
        if (this.nowIndexes.indexOf(index) === -1) {
          this.nowIndexes.push(index);
        } else {
          this.nowIndexes = _.remove(this.nowIndexes, (idx) => {
            return idx !== index;
          });
        }
        let nowObjArray = _.map(this.nowIndexes, (idx) => {
          return this.selections[idx];
        });
        this.$emit('on-change', nowObjArray);
      },
      checkActive (index) {
        return this.nowIndexes.indexOf(index) !== -1;
      }
    }
  };
</script>

<style type="text/css">
  .chooser-component {
    position: relative;
    display: inline-block;
  }

  .chooser-list li {
    display: inline-block;
    border: 1px solid #e3e3e3;
    height: 25px;
    line-height: 25px;
    padding: 0 8px;
    margin-right: 5px;
    border-radius: 3px;
    text-align: center;
    cursor: pointer;
  }

  .chooser-list li.active {
    border-color: #4fc08d;
    background: #4fc08d;
    color: #fff;
  }
</style>
