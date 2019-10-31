<template>
  <div class="controls-box">
    <div class="start-time">{{hadPlayTime.toFixed(2)}}</div>
    <div class="continue-time">
      <div class="track" ref="track"></div>
    </div>
    <div class="end-time">{{totalTime.toFixed(2)}}</div>
    <div class="rate">{{playRate}}</div>
    <div class="full-page">全屏</div>
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
      let trackWidth = (width / 24) * 10;
      let trackLength = percent * trackWidth;
      trackDom.style.width = trackLength + "px";
    }
  }
};
</script>

<style>
.controls-box {
  display: flex;
  line-height: 1;
}
.start-time {
  flex: 2;
  text-align: right;
  margin-left: 45px;
}
.continue-time {
  flex: 20;
  background-color: black;
  height: 3px;
  margin: 4px;
}
.continue-time .track {
  background-color: red;
  height: 3px;
  width: 0;
}
.end-time {
  flex: 3;
  text-align: left;
}
.rate {
  flex: 6;
}
.full-page {
  flex: 5;
  text-align: left;
}
</style>