<template>
  <div class="el-select">
    <div class="el-tag-box" @click.self="toggle">
      <div class="word" v-if="nowArr.length==0" @click.self="toggle">请选择</div>
      <div class="el-tag" v-for="(item,index) in nowArr">
        <span class="text">{{lists[item].text}}</span>
        <img class="close" src="../assets/icon/select-close.png" @click.stop="del(item)"/>
      </div>
    </div>
    <div class="el-icon" @click="toggle" ref="arrow">
      <span class="el-icon-box"></span>
      <img class="triangle" src="../assets/icon/select-triangle.png"/>
    </div>
    <transition name="fade">
      <div class="el-drop" v-if="isShow">
        <div class="el-drop-box">
          <ul class="el-drop-list">
            <li v-for="(item,index) in lists" @click.self="add(index)">
              <span>{{item.text}}</span>
              <img v-if="checkActive(index)" src="../assets/icon/select-check.png"/>
            </li>
          </ul>
        </div>
      </div>
    </transition>
  </div>
</template>

<script type="text/ecmascript-6">
  export default{
    props: {
      lists: {
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
        isShow: false,
        nowArr: []
      }
    },
    watch: {
      nowArr () {
        let backObj = [];
        for (let i = 0; i < this.nowArr.length; i++) {
          backObj.push({
            text: this.lists[this.nowArr[i]].text,
            value: this.lists[this.nowArr[i]].value
          });
        }
        this.$emit('on-change', backObj);
      },
      isShow () {
        if (this.isShow) {
          this.$refs.arrow.style.webkitTransform = 'rotate(180deg)';
          this.$refs.arrow.style.webkitTransition = 'transform .3s ease-in-out';
        } else {
          this.$refs.arrow.style.webkitTransform = '';
        }
      }
    },
    methods: {
      toggle () {
        this.isShow = !this.isShow;
      },
      add (index) {
        if (this.nowArr.indexOf(index) === -1) {
          this.nowArr.push(index);
        } else {
          for (let i = 0; i < this.nowArr.length; i++) {
            if (this.nowArr[i] === index) {
              this.nowArr.splice(i, 1);
              break;
            }
          }
        }
      },
      del (index) {
        for (let i = 0; i < this.nowArr.length; i++) {
          if (this.nowArr[i] == index) {
            this.nowArr.splice(i, 1);
            break;
          }
        }
      },
      checkActive (index) {
        return this.nowArr.indexOf(index) !== -1;
      }
    },
    mounted () {  //点击空白隐藏
      let _this = this;
      _this.$nextTick(function () {
        document.addEventListener('click', (e) => {
          if (!_this.$el.contains(e.target)) _this.isShow = false
        })
      });
    }
  }
</script>

<style scoped>
  .el-select {
    display: inline-block;
    width: 240px;
    padding: 4px;
    position: relative;
    background: #fff;
    border: 1px solid #bfcbd9;
    border-radius: 5px;
    -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
    -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
    transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  }

  .el-select:hover {
    border-color: #8c98a6;
  }

  .el-tag-box {
    max-width: 210px;
    text-align: left;
  }

  .el-tag-box .word {
    cursor: pointer;
    width: 100%;
    height: 26px;
    line-height: 26px;
    color: #99a6b4;
    font-size: 14px;
    padding-left: 2px;
  }

  .el-tag {
    display: inline-block;
    padding: 0 3px;
    line-height: 18px;
    box-sizing: border-box;
    margin: 3px 0 3px 2px;
    background-color: rgba(32, 160, 255, .1);
    border: 1px solid rgba(32, 160, 255, .2);
    border-radius: 4px;
    color: #20a0ff;
  }

  .el-tag > .text {
    font-size: 12px;
    line-height: 12px;
    vertical-align: middle;
  }

  .el-tag > .close {
    position: relative;
    top: -1px;
    width: 14px;
    cursor: pointer;
    vertical-align: middle;
  }

  .el-icon {
    position: absolute;
    font-size: 0;
    top: 0;
    right: 0;
    width: 30px;
    height: 100%;
    cursor: pointer;
  }

  .el-icon-box {
    line-height: 100%;
    vertical-align: middle;
    display: inline-block;
    height: 100%;
  }

  .el-icon > .triangle {
    width: 12px;
    vertical-align: middle;
  }

  .el-drop {
    position: absolute;
    left: -1px;
    top: 100%;
    width: 100%;
    z-index: 100;
    -webkit-transition: 0.3s;
    -o-transition: 0.3s;
    transition: 0.3s;
  }

  .el-drop-box {
    width: 100%;
    margin: 6px 0;
    padding: 6px 0;
    border: 1px solid #bfcbd9;
    background: #fff;
    border-radius: 2px;
    -webkit-box-shadow: 2px 2px 10px #bfcbd9;
    -moz-box-shadow: 2px 2px 10px #bfcbd9;
    box-shadow: 2px 2px 10px #bfcbd9;
    max-height: 200px;
    overflow-x: hidden;
    overflow-y: auto;
  }

  .fade-enter {
    -webkit-transform: translateY(10px);
    transform: translateY(10px);
    opacity: 0;
  }

  .fade-leave-active {
    -webkit-transform: translateY(10px);
    transform: translateY(10px);
    opacity: 0;
  }

  .el-drop-list > li {
    position: relative;
    width: 100%;
    text-align: left;
    padding: 0 10px;
    font-size: 14px;
    cursor: pointer;
    color: #48576a;
    height: 30px;
    line-height: 30px;
  }

  .el-drop-list > li > img {
    position: absolute;
    width: 20px;
    top: 2px;
    right: 30px;
  }

  .el-drop-list > li.active {
    color: #20a0ff;
  }

  .el-drop-list > li:hover {
    background: #e4e8f1;
  }

</style>
