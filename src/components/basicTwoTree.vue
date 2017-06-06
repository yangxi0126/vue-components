<template>
  <div class="tree-main">
    <div class="basic-tree-left">
      <div class="basic-tree-title">
        可选
      </div>
      <div class="basic-main-box">
        <div class="search-input-box">
          <input type="text" v-model="searchLeft"/>
          <img class="search" src="../assets/basicTree/basicTreeSearch.png"/>
        </div>
        <div class="basic-list-box">
          <ul class="basic-list-items">
            <li v-for="(item,index) in leftData" v-if="item.show" :data-id="item.id" @click="checkEvt(index,'left')">
              <img v-if="item.checked" src="../assets/basicTree/check_true.png"/>
              <img v-if="!item.checked" src="../assets/basicTree/check_false.png"/>
              <span>{{item.text}}</span>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <div class="basic-tree-middle">
      <img class="basic-left-img" src="../assets/basicTree/leftTriangle.png" @click="transfer('left')"/>
      <img class="basic-right-img" src="../assets/basicTree/rightTriangle.png" @click="transfer('right')"/>
    </div>
    <div class="basic-tree-right">
      <div class="basic-tree-title">
        已选
      </div>
      <div class="basic-main-box">
        <div class="search-input-box">
          <input type="text" v-model="searchRight"/>
          <img class="search" src="../assets/basicTree/basicTreeSearch.png"/>
        </div>
        <div class="basic-list-box">
          <ul class="basic-list-items">
            <li v-for="(item,index) in rightData" v-if="item.show" :data-id="item.id" @click="checkEvt(index,'right')">
              <img v-if="item.checked" src="../assets/basicTree/check_true.png"/>
              <img v-if="!item.checked" src="../assets/basicTree/check_false.png"/>
              <span>{{item.text}}</span>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default{
    props: {
      commonData: {
        type: Array,
        default: []
      }
    },
    data () {
      return {
        leftData: [],
        rightData: [],
        searchLeft: '',
        searchRight: ''
      }
    },
    mounted () {
      let me = this;
      me.$nextTick(function () {
        me.commonData.forEach(function (val) {
          val.show = true;
          if (val.checked) {
            val.checked = false;
            me.rightData.push(val);
          } else {
            me.leftData.push(val);
          }
        });
        me.leftData.sort(function (a, b) {
          return a.id - b.id;
        });
      });
    },
    methods: {
      checkEvt (index, type) {
        let me = this;
        if (type == 'left') {
          me.leftData[index].checked = !me.leftData[index].checked;
        } else {
          me.rightData[index].checked = !me.rightData[index].checked;
        }
      },
      transfer (type) {
        let me = this;
        if (type == 'left') {
          for (let i = 0; i < me.leftData.length; i++) {
            if (me.leftData[i].checked) {
              me.leftData[i].checked = false;
              me.rightData.push(me.leftData[i]);
              me.leftData.splice(i, 1);
              i--;
            }
          }
        } else {
          for (let i = 0; i < me.rightData.length; i++) {
            if (me.rightData[i].checked) {
              me.rightData[i].checked = false;
              me.leftData.push(me.rightData[i]);
              me.rightData.splice(i, 1);
              i--;
            }
          }
          me.leftData.sort(function (a, b) {
            return a.id - b.id;
          });
        }
      }
    },
    watch: {
      'searchLeft': function (content) {
        let me = this;
        let val = content.trim();
        if (val == '') {
          me.leftData.forEach(function (val) {
            val.show = true;
          });
        } else {
          me.leftData.forEach(function (val) {
            if (val.text == content || val.label == content) {
              val.show = true;
            } else {
              val.show = false;
            }
          });
        }
      },
      'searchRight': function (content) {
        let me = this;
        let val = content.trim();
        if (val == '') {
          me.rightData.forEach(function (val) {
            val.show = true;
          });
        } else {
          me.rightData.forEach(function (val) {
            if (val.text == content || val.label == content) {
              val.show = true;
            } else {
              val.show = false;
            }
          });
        }
      }
    }
  }
</script>

<style scoped>
  .tree-main {
    width: 650px;
    height: 382px;
    background: #fff;
  }

  .tree-main:after {
    display: block;
    content: "";
    width: 0;
    height: 0;
    overflow: hidden;
    clear: both;
  }

  .basic-tree-left, .basic-tree-middle {
    float: left;
  }

  .basic-tree-right {
    float: right;
  }

  .basic-tree-left, .basic-tree-right {
    width: 275px;
    height: 380px;
    border: 1px solid #D7D7D7;
    border-radius: 4px;
    overflow-x: hidden;
    overflow-y: auto;
  }

  .basic-tree-middle {
    position: relative;
    width: 80px;
    height: 380px;
    margin-left: 8px;
  }

  .basic-tree-middle .basic-left-img {
    position: absolute;
    cursor: pointer;
    width: 20px;
    left: 30px;
    top: 145px;
  }

  .basic-tree-middle .basic-right-img {
    position: absolute;
    cursor: pointer;
    width: 20px;
    left: 30px;
    top: 185px;
  }

  .basic-tree-title {
    width: 100%;
    height: 38px;
    line-height: 38px;
    background: #F6F8FA;
    text-align: left;
    text-indent: 20px;
    color: #222;
    font-size: 14px;
  }

  .basic-main-box .search-input-box {
    position: relative;
    width: 235px;
    height: 30px;
    margin: 20px;
  }

  .basic-main-box .search-input-box input {
    width: 190px;
    height: 30px;
    padding: 0 25px 0 12px;
    background-color: #fff;
    border: 1px solid #ccc;
    border-radius: 4px;
  }

  .basic-main-box .search-input-box input:focus {
    border-color: #66afe9;
    outline: 0;
    -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075), 0 0 8px rgba(102, 175, 233, .6);
    box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075), 0 0 8px rgba(102, 175, 233, .6);
  }

  .basic-main-box .search-input-box .search {
    position: absolute;
    right: 10px;
    top: 8px;
    width: 15px;
  }

  .basic-list-items {
    width: 100%;
    margin: 0 auto;
    list-style: none;
  }

  .basic-list-items > li {
    display: block;
    width: 100%;
    padding: 3px 20px;
    cursor: pointer;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }

  .basic-list-items > li:hover {
    background: #F6F8FA;
  }

  .basic-list-items > li:after {
    display: block;
    content: "";
    width: 0;
    height: 0;
    overflow: hidden;
    clear: both;
  }

  .basic-list-items > li img {
    display: inline-block;
    float: left;
    margin: 0 10px 0 2px;
    width: 20px;
  }

  .basic-list-items > li span {
    width: 205px;
    display: inline-block;
    height: 20px;
    line-height: 20px;
    text-align: left;
    font-size: 14px;
    float: left;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
</style>
