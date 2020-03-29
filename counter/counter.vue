<!--
计数功能

-->
<template>
  <!-- 计数功能组件 -->
  <div class="counter-component">
    <!-- minus -->
    <div @click="minus" class="counter-btn"> -</div>
    <!-- number show -->
    <div class="counter-show">
      <input v-model="number" @keyup="fixNumber" type="text">
    </div>
    <!-- plus -->
    <div @click="add" class="counter-btn"> +</div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    // 最大最小值：默认
    props: {
      max: {
        type: Number,
        default: 5
      },
      min: {
        type: Number,
        default: 1
      }
    },
    data () {
      return {
        number: this.min
      };
    },
    watch: {
      number () {
        this.$emit('on-change', this.number);
      }
    },
    methods: {
      fixNumber () {
        let fix;
        if ((typeof this.number) === 'string') {
          fix = Number(this.number.replace(/\D/g, ''));
        } else {
          fix = this.number;
        }
        if ((fix > this.max) || (fix < this.this.min)) {
          fix = this.min;
        }
        this.number = fix;
      },
      minus () {
        if (this.number <= this.min) {
          return;
        }
        this.number--;
      },
      add () {
        if (this.number >= this.max) {
          return;
        }
        this.number++;
      }
    }
  };
</script>

<style type="text/css">
  .counter-component {
    position: relative;
    display: inline-block;
    overflow: hidden;
    vertical-align: middle;
  }

  .counter-show {
    float: left;
  }

  .counter-show input {
    border: none;
    border-top: 1px solid #e3e3e3;
    border-bottom: 1px solid #e3e3e3;
    height: 23px;
    line-height: 23px;
    width: 30px;
    outline: none;
    text-indent: 4px;
  }

  .counter-btn {
    border: 1px solid #e3e3e3;
    float: left;
    height: 25px;
    line-height: 25px;
    width: 25px;
    text-align: center;
    cursor: pointer;
  }

  .counter-btn:hover {
    border-color: #4fc08d;
    background: #4fc08d;
    color: #fff;
  }

</style>
