<template>
  <div class="chooser-component">
    <ul class="chooser-list">
      <li v-for="(item,index) in single" :class="{active:index==nowIndex}" @click="clickEvt(index)">{{item.text}}</li>
    </ul>
  </div>
</template>

<script type="text/ecmascript-6">
  export default{
    props: {
      single: {
        type: Array,
        default: [
          {
            text: 'test',
            value: 'test'
          }
        ]
      }
    },
    data () {
      return {
        nowIndex: 0
      }
    },
    methods: {
      clickEvt (index) {
        this.nowIndex = index;
        this.$emit('on-change', this.single[index]);
      }
    }
  }
</script>

<style scoped>
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
