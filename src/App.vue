<template>
  <div id="app">
    <div class="components-box">
      <p>下拉框 select</p>
      <v-select :lists="selections" @on-change="selectChange($event)"></v-select>
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
      <p>轮播 slide</p>
      <v-slide :slides="slides" :interval="intervalTime" @on-change="slideChange($event)"></v-slide>
    </div>
  </div>
</template>

<script>
  import vSelect from './components/select'
  import vSingle from './components/single'
  import vMultiple from './components/multiple'
  import vSlide from './components/slide'

  export default {
    components: {
      vSelect,
      vSingle,
      vMultiple,
      vSlide
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
        intervalTime: 3000
      }
    },
    methods: {
      selectChange (event) {
        console.log("select");
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
        console.log("slide");
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

  .components-box p {
    margin: 10px;
    padding: 10px;
    background: #4fc08d;
    color: #fff;
  }
</style>
