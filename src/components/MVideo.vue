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
      <div class="center-progress">
        <span class="start-time">{{timeDisplay}}</span>
        <span class="continue-time">————</span>
        <span class="end-time">{{totalTime}}</span>
        <span class="rate" @click="changeRate">{{playRate}}</span>
        <span class="full-page" @click.self.stop="fullPage">全屏</span>
      </div>
      <div class="line">
        <div class="wrap" ref="progressWrap">
          <div class="progress" ref="progress"></div>
        </div>
      </div>
      <div class="mock" @click="clickMock"></div>
      <div class="text-container" @click="clickMock" v-show="showText">{{DomText}}</div>
    </div>
    <div class="detail">商品详情展示</div>
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
export default {
  data() {
    return {
      width: document.documentElement.clientWidth,
      height: "300",
      refDom: null,
      DomText: "播放",
      playRate: "倍速",
      isPause: true,
      showText: false,
      // 视频总时长
      totalTime: 0,
      // 已经播放过的视频时间
      currentTime: 0,
      //当前播放时间
      timeDisplay: 0,
      num: 0,
      goFlag: null,
      clientWidth: 0
    };
  },
  mounted() {
    this.refDom = this.$refs.video;
    this.clientWidth = document.documentElement.clientWidth;
    setTimeout(() => {
      this.totalTime = this.refDom.duration;
    }, 60);
    this.refDom.addEventListener(
      "timeupdate",
      () => {
        //用秒数来显示当前播放进度
        let playSecond = Math.floor(video.currentTime.toFixed(2));

        this.timeDisplay = playSecond;
      },
      false
    );
  },
  methods: {
    // 播放/暂停
    clickMock() {
      if (this.refDom.paused) {
        console.log("播放中- :");
        console.log("currentTime", this.refDom.currentTime);
        this.refDom.play();
        this.DomText = "暂停";
        if (this.showText) {
          let _this = this;
          setTimeout(() => {
            _this.showText = false;
          }, 500);
        }

        this.go();
      } else {
        console.log("暂停");
        console.log("currentTime", this.refDom.currentTime);
        clearInterval(this.goFlag);
        this.refDom.pause();
        this.DomText = "播放";
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
    changeRate() {
      console.log("changeRate");
      this.refDom.playbackRate = 2;
      this.playRate = 2.0;
    },
    // 全屏
    fullPage() {
      console.log("fullPage");
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
.center-progress {
  position: absolute;
  bottom: 65px;
  left: 110px;
  color: yellow;
  z-index: 100;
}
.center-progress .rate {
  margin: 0 10px;
}
.center-progress .full-page {
  background: aqua;
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
  background: #f2f2f2;
  border: 1px solid #ccc;
  border-radius: 100%;
  width: 50px;
  height: 50px;
  align-items: center;
  justify-content: center;
  display: flex;
}
</style>