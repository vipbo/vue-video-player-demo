<template>
  <div>
    <div class="video-box">
      <video
        id="video"
        ref="video"
        src="../assets/mao.mp4"
        :controls="false"
        :width="width"
        :height="height"
        poster="../assets/post.jpg"
      >您的浏览器不支持 video 标签。</video>
      <!-- 自定义播放进度条 -->
      <div class="line">
        <div class="wrap" ref="progressWrap">
          <div class="progress" ref="progress"></div>
        </div>
      </div>
      <div class="mock" @click="clickMock"></div>
      <!-- 播放/暂停按钮 -->
      <div class="text-container" @click="clickMock" v-show="showText">
        <!-- {{DomText}} -->
        <img :src="srcUrl" alt="暂停/播放" />
      </div>
    </div>
    <m-controls
      :hadPlayTime="timeDisplay"
      :totalTime="totalTime"
      @changePalyRate="changeRate"
      @fullScreen="fullPage"
      v-show="showText"
    ></m-controls>
    <!-- <div class="detail">商品详情展示</div> -->
  </div>
</template>

<script>
//进入全屏
function FullScreen() {
  var ele = document.documentElement;
  if (ele.requestFullscreen) {
    ele.requestFullscreen();
    //For Firefox
  } else if (ele.mozRequestFullScreen) {
    ele.mozRequestFullScreen();
    //For Webkit
  } else if (ele.webkitRequestFullScreen) {
    ele.webkitRequestFullScreen();
  }
}
import MControls from "./MControls";
import zanting from "../assets/zanting_1.png";
import bofang from "../assets/bofang_2.png";
export default {
  data() {
    return {
      width: document.documentElement.clientWidth,
      height: "300",
      refDom: null,
      DomText: "播放",
      playRate: "倍速",
      showText: false,
      // 视频总时长
      totalTime: 0,
      //当前播放时间
      timeDisplay: 0,
      goFlag: null,
      clientWidth: 0,
      showControls: false,
      srcUrl: ""
    };
  },
  components: {
    MControls
  },
  mounted() {
    this.refDom = this.$refs.video;
    this.clientWidth = document.documentElement.clientWidth;
    setTimeout(() => {
      this.totalTime = this.refDom.duration;
    }, 300);
    this.refDom.addEventListener(
      "timeupdate",
      () => {
        //用秒数来显示当前播放进度
        this.timeDisplay = video.currentTime;
      },
      false
    );
  },
  methods: {
    // 播放/暂停
    clickMock() {
      this.showControls = true;
      if (this.refDom.paused) {
        this.refDom.play();
        this.DomText = "暂停";
        this.srcUrl = zanting;
        if (this.showText) {
          let _this = this;
          setTimeout(() => {
            _this.showText = false;
          }, 500);
        }

        this.go();
      } else {
        clearInterval(this.goFlag);
        this.refDom.pause();
        this.DomText = "播放";
        this.srcUrl = bofang;
        if (!this.showText) {
          let _this = this;
          setTimeout(() => {
            _this.showText = true;
          }, 100);
        }
      }
      return false;
    },
    // progress
    go() {
      // 获取进度条
      let dom = this.$refs.progress;
      // 获取视频视频总时间
      let duration = this.refDom.duration;
      let progressWrapDom = this.$refs.progressWrap;
      this.goFlag = setInterval(() => {
        // 视频总时间 已播放时间，计算百分比
        let percent = this.timeDisplay / duration;
        dom.style.width = this.clientWidth * percent + "px";
      }, 60);
    },
    // 改变倍速
    changeRate(rate) {
      this.refDom.playbackRate = rate;
    },
    // 全屏
    fullPage() {
      FullScreen();
    }
  }
};
</script>

<style scoped >
@import "./public.css";

.detail {
  width: 99%;
  height: 600px;
  margin-top: 10px;
  border: 1px solid #000;
}
.video-box {
  width: 100%;
  height: 300px;
  position: relative;
}
.line {
  position: absolute;
  left: 0;
  bottom: 47px;
  display: none;
}
.line .wrap {
  background-color: black;
  height: 5px;
  cursor: pointer;
}
.line .progress {
  background-color: red;
  width: 0px;
  height: 5px;
}

.mock {
  background-color: rgba(100, 100, 100, 0);
  width: 100%;
  height: 190px;
  position: absolute;
  top: 53px;
  left: 0;
}
.text-container {
  position: absolute;
  top: 120px;
  left: 160px;
  background: transparent;
  border: 1px solid #ccc;
  border-radius: 100%;
  width: 50px;
  height: 50px;
  align-items: center;
  justify-content: center;
  display: flex;
}
.text-container img {
  width: 30px;
  height: 30px;
  border-radius: 100%;
}
</style>