<template>
  <div class="controls-box">
    <div class="start-time">{{hadPlayTime.toFixed(2)}}</div>
    <div class="continue-time">
      <div class="track" ref="track"></div>
    </div>
    <div class="end-time">{{totalTime.toFixed(2)}}</div>
    <div class="rate" @click="changePlayRate">{{playRate}}</div>
    <div class="full-page" @click="fullScreen">
      <img src="../assets/big.png" alt="全屏" />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    hadPlayTime: [Number, String],
    totalTime: [Number, String]
  },
  data() {
    return {
      width: document.documentElement.clientWidth,
      playRate: "倍速",
      percent: 0
    };
  },
  watch: {
    hadPlayTime(newVal, oldVal) {
      let percent = newVal / this.totalTime;
      this.percent = percent;
      this.playContinue();
    }
  },

  methods: {
    playContinue() {
      let trackDom = this.$refs.track;
      let { width, percent } = this;
      let trackWidth = (width / 24) * 12.5;
      let trackLength = percent * trackWidth;
      trackDom.style.width = trackLength + "px";
    },
    //倍速
    changePlayRate() {
      let { playRate } = this;
      if (playRate == "倍速") {
        this.playRate = 0.8;
        this.$emit("changePalyRate", 0.8);
        return false;
      }
      if (playRate == 0.8) {
        this.playRate = 1;
        this.$emit("changePalyRate", 1);
        return false;
      }
      if (playRate == 1) {
        this.playRate = 1.5;
        this.$emit("changePalyRate", 1.5);
        return false;
      }
      if (playRate == 1.5) {
        this.playRate = 2;
        this.$emit("changePalyRate", 2);
        return false;
      }
      if (playRate == 2) {
        this.playRate = "倍速";
        this.$emit("changePalyRate", 1);
        return false;
      }
    },
    //全屏
    fullScreen() {
      this.$emit("fullScreen");
    }
  }
};
</script>

<style>
.controls-box {
  display: flex;
  line-height: 1;
  position: absolute;
  width: 100%;
  top: 278px;
  left: -10px;
  color: #fff;
  font-size: 12px;
}
.start-time {
  flex: 2;
  text-align: right;
  margin-left: 45px;
  margin-top: 5px;
}
.continue-time {
  flex: 20;
  height: 3px;
  margin: 4px;
  background-color: #f2f2f2;
  border-radius: 2px;
  margin-top: 9px;
}
.continue-time .track {
  background-color: red;
  height: 3px;
  width: 0;
}
.end-time {
  flex: 3;
  text-align: left;
  margin-top: 5px;
}
.rate {
  /* flex: 6; */
  border: 1px solid #ffffff;
  padding: 3px 0;
  border-radius: 30px 28px;
  width: 35px;
  margin: 0 5px;
}
.full-page {
  /* flex: 5; */
  /* text-align: left; */
  /* margin-top: 5px; */
  /* background-image: url('../assets/quanping.png'); */
  /* background-repeat: no-repeat; */
}
.full-page img {
  width: 20px;
  height: 18px;
}
</style>