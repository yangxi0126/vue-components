<template>
  <div class="slide-show" @mouseover="clearInv" @mouseout="runInv">
    <div class="slide-img">
      <router-link :to="{path:'/'}">
        <transition name="slide-trans">
          <img v-if="isShow" :src="slides[nowIndex].src" alt="slides[nowIndex].title">
        </transition>
        <transition name="slide-trans-old">
          <img v-if="!isShow" :src="slides[nowIndex].src" alt="slides[nowIndex].title">
        </transition>
      </router-link>
    </div>
    <h2>{{slides[nowIndex].title}}</h2>
    <ul class="slide-pages">
      <li @click="goto(prevPic)">&lt;</li>
      <li v-for="(item,index) in slides" @click="goto(index)">
        <a :class="{active:index==nowIndex}">{{index+1}}</a>
      </li>
      <li @click="goto(nextPic)">&gt;</li>
    </ul>
  </div>
</template>

<script type="text/ecmascript-6">
  export default{
    props: {
      slides: {
        type: Array,
        default: []
      },
      interval: {
        type: Number,
        default: 1000
      }
    },
    data () {
      return {
        nowIndex: 0,
        isShow: true,
        slideName: null
      }
    },
    methods: {
      goto (index) {
        let _this = this;
        _this.isShow = false;
        setTimeout(() => {
          _this.isShow = true;
          _this.nowIndex = index;
          _this.$emit('on-change', index);
        }, 10)
      },
      runInv () {
        let _this = this;
        _this.slideName = setInterval(function () {
          _this.goto(_this.nextPic);
        }, _this.interval);
      },
      clearInv () {
        clearInterval(this.slideName);
      }
    },
    computed: {
      prevPic () {
        if (this.nowIndex == 0) {
          return this.slides.length - 1;
        } else {
          return this.nowIndex - 1;
        }
      },
      nextPic () {
        if (this.nowIndex == this.slides.length - 1) {
          return 0;
        } else {
          return this.nowIndex + 1;
        }
      }
    },
    mounted () {
      this.$nextTick(function () {
        this.runInv();
      });
    }
  }
</script>

<style scoped>
  .slide-trans-enter-active {
    transition: all .5s;
  }

  .slide-trans-enter {
    transform: translateX(900px);
  }

  .slide-trans-old-leave-active {
    transition: all .5s;
    transform: translateX(-900px);
  }

  .slide-show {
    position: relative;
    margin: 0 auto;
    width: 900px;
    height: 500px;
    overflow: hidden;
  }

  .slide-show h2 {
    position: absolute;
    width: 100%;
    color: #fff;
    background: #000;
    opacity: .5;
    bottom: 0;
    height: 30px;
    line-height: 30px;
    text-align: left;
    padding-left: 15px;
  }

  .slide-img {
    width: 100%;
    height: 100%;
    position: relative;
  }

  .slide-img img {
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
  }

  .slide-pages {
    position: absolute;
    bottom: 10px;
    right: 15px;
  }

  .slide-pages li {
    display: inline-block;
    padding: 0 10px;
    cursor: pointer;
    color: #fff;
  }

  .slide-pages li .active {
    text-decoration: underline;
  }
</style>
