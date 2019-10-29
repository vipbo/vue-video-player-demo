<template>
  <div class="hello">
    <!-- <video src="../assets/mao.mp4" controls="controls" width="300" height="300">您的浏览器不支持 video 标签。</video> -->
    <!-- <hr /> -->
    <video-player
      class="video-player-box vjs-big-play-centered"
      ref="videoPlayer"
      :options="playerOptions"
      :playsinline="true"
      customEventName="customstatechangedeventname"
      @play="onPlayerPlay($event)"
      @pause="onPlayerPause($event)"
      @ended="onPlayerEnded($event)"
      @waiting="onPlayerWaiting($event)"
      @playing="onPlayerPlaying($event)"
      @loadeddata="onPlayerLoadeddata($event)"
      @timeupdate="onPlayerTimeupdate($event)"
      @canplay="onPlayerCanplay($event)"
      @canplaythrough="onPlayerCanplaythrough($event)"
      @statechanged="playerStateChanged($event)"
      @ready="playerReadied"
    ></video-player>
  </div>
</template>

<script>
import { videoPlayer } from "vue-video-player";
export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  components: {
    videoPlayer
  },
  data() {
    return {
      // videojs options
      playerOptions: {
        width: document.documentElement.clientWidth,
        height: 300,
        muted: true,
        language: "en",
        playbackRates: [0.7, 1.0, 1.5, 2.0],
        sources: [
          {
            type: "video/mp4",
            src:
              "https://cdn.theguardian.tv/webM/2015/07/20/150716YesMen_synd_768k_vp8.webm"
          }
        ],
        poster: "https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=939047871,4111159124&fm=11&gp=0.jpg"
      }
    };
  },
  mounted() {
    console.log("this is current player instance object", this.player);
  },
  computed: {
    player() {
      return this.$refs.videoPlayer.player;
    }
  },
  methods: {
    // listen event
    onPlayerPlay(player) {
      console.log("player play!", player);
    },
    onPlayerPause(player) {
      console.log("player pause!", player);
    },
    onPlayerEnded() {},
    onPlayerWaiting() {},
    onPlayerPlaying() {},
    onPlayerLoadeddata() {},
    onPlayerTimeupdate() {},
    onPlayerCanplay() {},
    onPlayerCanplaythrough() {},
    // ...player event

    // or listen state event
    playerStateChanged(playerCurrentState) {
      // console.log('player current update state', playerCurrentState)
    },

    // player is ready
    playerReadied(player) {
      console.log("the player is readied", player);
      // you can use it to do something...
      // player.[methods]
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.video-player-box {
  width: 300px;
  height: 300px;
}
</style>
