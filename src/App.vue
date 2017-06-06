<template>
  <div id="app">
    <div class="components-box">
      <p>下拉框 select</p>
      <v-select :lists="selections" @on-change="selectChange($event)"></v-select>
    </div>
    <div class="components-box">
      <p>下拉多选 selectMultiple</p>
      <v-smultiple :lists="selections" @on-change="selectMultiChange($event)"></v-smultiple>
    </div>
    <div class="components-box">
      <p>单选框 single</p>
      <v-single :single="selections" @on-change="singleChange($event)"></v-single>
    </div>
    <div class="components-box">
      <p>复选框 multiple</p>
      <v-multiple :multiple="selections" @on-change="multipleChange($event)"></v-multiple>
    </div>
    <div class="components-box">
      <p>弹窗 modal</p>
      <div class="app-btn" @click="showEvt">show modal</div>
      <v-modal :isShow="isShow" @on-change="closeEvt"></v-modal>
    </div>
    <div class="components-box">
      <p>分页 page</p>
      <v-page :total="80" :current.sync="1" :dispaley="10" @on-change="pageChange($event)"></v-page>
    </div>
    <div class="components-box">
      <p>树形结构 tree(注意此处传的值时item，不是整个数组)</p>
      <div style="width: 300px;margin: 0 auto;">
        <ul class="filetree treeview">
          <v-tree :tree="item" :index.number="index" v-for="(item,index) in tree" :key="index"></v-tree>
        </ul>
      </div>
    </div>
    <div class="components-box">
      <p>轮播 slide</p>
      <v-slide :slides="slides" :interval="intervalTime" @on-change="slideChange($event)"></v-slide>
    </div>
    <div class="components-box">
      <p>简单左右树 basicTwoTree</p>
      <div style="width: 650px;margin: 0 auto;">
        <basic-two-tree :commonData="basicTwoTree"></basic-two-tree>
      </div>
    </div>
  </div>
</template>

<script>
  import vSelect from './components/select'
  import vSmultiple from './components/selectMultiple'
  import vSingle from './components/single'
  import vMultiple from './components/multiple'
  import vSlide from './components/slide'
  import vModal from './components/modal'
  import vPage from './components/page'
  import vTree from './components/tree'
  import basicTwoTree from './components/basicTwoTree'

  export default {
    components: {
      vSelect,
      vSmultiple,
      vSingle,
      vMultiple,
      vSlide,
      vModal,
      vPage,
      vTree,
      basicTwoTree
    },
    name: 'app',
    data () {
      return {
        selections: [
          {
            text: '北京',
            value: 0
          },
          {
            text: '上海',
            value: 1
          },
          {
            text: '广州',
            value: 2
          },
          {
            text: '深圳',
            value: 3
          }
        ],
        slides: [
          {
            src: require('./assets/slidePic/pic1.jpg'),  //js中，require的图片才会被webpack正确打包
            title: 'pic1',
            href: 'www.baidu.com'
          },
          {
            src: require('./assets/slidePic/pic2.jpg'),
            title: 'pic2',
            href: 'www.baidu.com'
          },
          {
            src: require('./assets/slidePic/pic3.jpg'),
            title: 'pic3',
            href: 'www.baidu.com'
          },
          {
            src: require('./assets/slidePic/pic4.jpg'),
            title: 'pic4',
            href: 'www.baidu.com'
          }
        ],
        intervalTime: 3000,
        isShow: false,
        tree: [
          {
            label: 'Folder 1',
            value: 'Folder 1',
            children: [
              {
                label: 'Item 1.1',
                value: 'Item 1.1',
                last: true
              }
            ]
          },
          {
            label: 'Folder 2',
            value: 'Folder 2',
            children: [
              {
                label: 'Subfolder 2.1',
                value: 'Subfolder 2.1',
                children: [
                  {
                    label: 'File 2.1.1',
                    value: 'File 2.1.1'
                  },
                  {
                    label: 'File 2.1.2',
                    value: 'File 2.1.2',
                    children: [
                      {
                        label: 'File 2.1.2.1',
                        value: 'File 2.1.2.1',
                        last: true
                      }
                    ]
                  },
                  {
                    label: 'File 2.1.3',
                    value: 'File 2.1.3',
                    last: true
                  }
                ]
              },
              {
                label: 'File 2.2',
                value: 'File 2.2',
                last: true
              }
            ]
          },
          {
            label: 'Folder 3 (closed at start)',
            value: 'Folder 3',
            children: [
              {
                label: 'File 3.1',
                value: 'File 3.1',
                last: true
              }
            ]
          },
          {
            label: 'File 4',
            value: 'File 4'
          },
          {
            label: 'File 5',
            value: 'File 5',
            last: true
          }
        ],
        basicTwoTree: [
          {
            id: 1,
            text: '北京',
            label: 'beijing',
            checked: false
          },
          {
            id: 2,
            text: '上海',
            label: 'shanghai',
            checked: true
          },
          {
            id: 3,
            text: '广州',
            label: 'guangzhou',
            checked: true
          },
          {
            id: 4,
            text: '成都',
            label: 'chengdu',
            checked: false
          },
          {
            id: 5,
            text: '深圳',
            label: 'shenzhen',
            checked: false
          },
          {
            id: 6,
            text: '武汉',
            label: 'wuhan',
            checked: false
          }
        ]
      }
    },
    methods: {
      selectChange (event) {
        console.log("select");
        console.log(event);
      },
      selectMultiChange (event) {
        console.log("selectMulti");
        console.log(event);
      },
      singleChange (event) {
        console.log("single");
        console.log(event);
      },
      multipleChange (event) {
        console.log("multiple");
        console.log(event);
      },
      slideChange (event) {
//        console.log("slide");
//        console.log(event);
      },
      showEvt () {
        this.isShow = true;
      },
      closeEvt () {
        this.isShow = false;
      },
      pageChange (event) {
        console.log(event);
      },
      treeChange (event) {
        console.log(event);
      }
    }
  }
</script>

<style>
  @import "./assets/reset.css";

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 20px;
  }

  .components-box {
    display: block;
    width: 100%;
    margin: 30px 0;
  }

  .components-box > p {
    margin: 10px;
    padding: 10px;
    background: #4fc08d;
    color: #fff;
  }

  .app-btn {
    width: 120px;
    height: 35px;
    line-height: 35px;
    margin: 0 auto;
    cursor: pointer;
    font-size: 14px;
    color: #fff;
    background: #4fc08d;
  }
</style>
