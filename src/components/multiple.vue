<template>
  <div class="chooser-component">
    <ul class="chooser-list">
      <li v-for="(item,index) in multiple" :class="{active:checkActive(index)}" @click="clickEvt(index)">{{item.text}}</li>
    </ul>
  </div>
</template>

<script type="text/ecmascript-6">
  export default{
    props: {
      multiple: {
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
        nowArr: [],
      }
    },
    methods: {
      clickEvt (index) {
        if (this.nowArr.indexOf(index) == -1) {  //不在其中，没有选中
          this.nowArr.push(index);
        } else {  //在其中，已经选中了，要取消选中
          for (let i = 0; i < this.nowArr.length; i++) {
            if (this.nowArr[i] == index) {
              this.nowArr.splice(i, 1);
              break;
            }
          }
        }
        let returnArr = [];
        for (let i = 0; i < this.nowArr.length; i++) {
          returnArr.push({
            text: this.multiple[this.nowArr[i]].text,
            value: this.multiple[this.nowArr[i]].value
          });
        }
        this.$emit('on-change', returnArr);
      },
      checkActive (index) {
        return this.nowArr.indexOf(index) !== -1;
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
