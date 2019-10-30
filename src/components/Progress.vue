<template>
  <div class="box">
    <div class="wrap">
      <div class="progress" ref="progress"></div>
    </div>
    <hr />
    <button @click="bengin">{{btnText}}</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      flag: true,
      sFlag: null,
      btnText: "开始",
      num: 0,
      clientWidth: 0
    };
  },
  mounted() {
    this.clientWidth = document.documentElement.clientWidth;
    console.log("width:", this.clientWidth);
  },
  methods: {
    go() {
      let dom = this.$refs.progress;

      this.sFlag = setInterval(() => {
        if (this.num >= this.clientWidth) {
          clearInterval(this.sFlag);
        } else {
          this.num = this.num + 2;
          dom.style.width = this.num + "px";
        }
      }, 60);
    },
    bengin() {
      if (this.btnText === "开始") {
        this.go();
        this.btnText = "暂停";
      } else {
        clearInterval(this.sFlag);
        this.btnText = "开始";
      }
    }
  }
};
</script>

<style>
.box .wrap {
  background-color: black;
  height: 5px;
  cursor: pointer;
}
.box .progress {
  background-color: red;
  width: 0px;
  height: 5px;
}
</style>