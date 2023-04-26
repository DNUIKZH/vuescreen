<template>
  <!-- 轮播图加导航 -->
  <div class="firstPage">
    <!-- 轮播图 -->
    <div class="block text-center">
      <el-carousel height="600px" interval="4000">
        <el-carousel-item v-for="item in swipers" :key="item.id">
          <img :src="item.imgurl">
        </el-carousel-item>

        <el-carousel-item>
          <video id="video" src="https://www.neusoft.edu.cn/attachment/core/label/2023_04/18_09/6fd48bf96aae434f.mp4"
            loop="true" autoplay="true" muted="true" playsinline="true" webkit-playsinline="true" x-webkit-airplay="allow"
            airplay="allow" x5-video-orientation="h5" x5-video-player-type="h5" x5-video-player-fullscreen="true"
            preload="auto" data-object-fit="fill"></video>
        </el-carousel-item>
      </el-carousel>
    </div>
    <!-- 顶部导航 -->
    <div :class="{ head: true, NavTopping: isTop }" :style="{ opacity: headNull }">
      <a href="" style="font-size: 20px;">大连东软信息学院(LOGO)</a>
      <a href="">
        <div class="title login">登录</div>
      </a>
      <a href="">
        <div class="title home">首页</div>
      </a>
      <a href="">
        <div class="title up">注册</div>
      </a>
    </div>
    <!-- 返回顶部 -->
    <div class="GoTop">
      <a href="javascript:window.scrollTo(0,0)">
        <transition name="Top">
          <div class="BackTop" v-show="toTop"><img src="../src/assets/imges/返回顶部.svg"></div>
        </transition>
      </a>
    </div>
  </div>
  <!-- 首页主体部分 -->
  <div class="main">
      主页主体部分<br>
      <h1>测试文字1</h1><br>
      <h1>测试文字2</h1><br>
      <h1>测试文字3</h1><br>
    </div>
</template>
<script lang="ts">
export default {
  name: 'VueActiveScreenApp',

  data() {
    return {
      isTop: false,
      toTop: false,
      headNull: 1,
      swipers: [
        {
          id: "01",
          imgurl: "/imges/2333.png"
        },
        {
          id: "02",
          imgurl: '/imges/2444.png'
        },
        {
          id: "03",
          imgurl: '/imges/2555.png'
        }
      ]
    };
  },

  mounted() {
    window.addEventListener("scroll", this.scrollToTop, true);
  },
  destroyed() {
    window.removeEventListener("scroll", this.scrollToTop, true);
  },
  methods: {
    scrollToTop() {
      let scrollTop =
        window.pageYOffset ||
        document.documentElement.scrollTop ||
        document.body.scrollTop;
      //为了计算距离顶部的高度，当高度大于50显示回顶部图标，小于50则隐藏
      if (scrollTop > 600) {
        this.isTop = true;
        this.toTop = true;
      } else {
        this.isTop = false;
        this.toTop = false;
      }
      if (scrollTop > 100 && scrollTop < 600) {
        this.headNull = 0;
      } else {
        this.headNull = 1;
      }
    },
  },
};
</script>

/* 轮播图css */
<style scoped>
.text-center {
  position: relative;
}

.demonstration {
  color: var(--el-text-color-secondary);

}

.el-carousel__item:nth-child(2n) {
  background-color: #99a9bf;
}

.el-carousel__item:nth-child(2n + 1) {
  background-color: #d3dce6;
}

.el-carousel__item img {
  width: 100%;
  height: 100%;
}

.el-carousel__item video {
  width: 100%;
}
</style>

/* 首页css */
<style lang="scss" scoped>
.head {
  height: 70px;
  width: 100%;
  background-color: rgba(255, 255, 255, .0);
  line-height: 65px;
  position: absolute;
  top: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-weight: bold;
  transition: all .5s;


  a {
    color: rgb(251, 251, 251);
    text-decoration: none;
  }

  .title {
    z-index: 1;
    height: 40px;
    width: 40px;
    position: absolute;
    top: 13.5px;
    line-height: 40px;
    text-align: center;
  }

  .login {
    right: 6rem;
  }

  .up {
    right: 3rem;
  }

  .home {
    left: 16rem;
  }

  &:hover {
    background-color: rgb(255, 255, 255);

    a {
      text-decoration: none;
      color: black;
    }

    a:hover {
      color: #00b0ff;
    }
  }
}

/* 导航置顶css*/

.NavTopping {
  position: fixed;
  top: 0;
  z-index: 999;
  // background-color: rgb(255, 255, 255);
  background: rgba(255, 172, 172, .0);
  background-image: radial-gradient(transparent 1px, #fff 1px);
  background-size: 4px 4px;
  backdrop-filter: saturate(50%) blur(4px);
  transition: all .5s;
  .login,.up,.home{
    background-color: rgba(255, 255,255, .4);
    border-radius: 6px;
  }

  a {
    color: black;
    background-color: rgba($color: #ffffff, $alpha: .4);
    border-radius: 8px;
  }

  &:hover {
    background: rgba(255, 255, 255, .0);
    background-image: radial-gradient(transparent 1px, #fff 1px);
    background-size: 4px 4px;
    backdrop-filter: saturate(50%) blur(4px);
  }
}

/* 返回顶部css */
.GoTop {
  .BackTop {
    width: 60px;
    height: 60px;
    line-height: 80px;
    background-color: rgb(255, 205, 251);
    text-align: center;
    position: fixed;
    right: 20px;
    display: block;
    color: rgb(255, 255, 255);
    font-weight: bold;
    border-radius: 50%;

    img {
      width: 50px;
      padding-top: 6px;
    }
  }

  .Top-enter-from,
  .Top-leave-to {
    opacity: 0;
  }

  .Top-enter-to,
  .Top-leave-from {
    opacity: 1;
  }

  .Top-enter-active,
  .Top-leave-active {
    transition: opacity .2s ease;
  }
}

/* 首页主体css */
.main {
  background-color: rgb(255, 255, 255);
  text-align: center;
  height: 1200px;
}
</style>

<style lang="scss" scoped>
.main{
  h1{
    width: 100%;
    height: 200px;
    font-size: 100px;
    margin: 0;
  }
}
</style>