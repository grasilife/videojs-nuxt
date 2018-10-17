<template>
<div>
  <div  :class="palyShow?'visible':'invisible'">
  <video
    id="my-player"
    class="video-js vjs-default-skin vjs-big-play-centered"
>
  <p class="vjs-no-js">
    To view this video please enable JavaScript, and consider upgrading to a
    web browser that
    <a href="http://videojs.com/html5-video-support/" target="_blank">
      supports HTML5 video
    </a>
  </p>
</video>
  </div>
  <div :class="!palyShow?'visible':'invisible'">
  <video
    id="my-player1"
    class="video-js vjs-default-skin vjs-big-play-centered"
>
  <p class="vjs-no-js">
    To view this video please enable JavaScript, and consider upgrading to a
    web browser that
    <a href="http://videojs.com/html5-video-support/" target="_blank">
      supports HTML5 video
    </a>
  </p>
</video>
  </div>

<button @click="cllick1">视频1</button>
<button @click="cllick2">视频2</button>
<button @click="cllick2">视频3</button>
<button @click="showClick">切换</button>
</div>
</template>

<script>
import Logo from "~/components/Logo.vue";
import "video.js/dist/video-js.css";
import videojs from "video.js";
import "videojs-flash";

export default {
  components: {
    Logo
  },
  data() {
    return {
      player: null,
      player1: null,
      palyShow: false,
      progressLast: 0
    };
  },
  methods: {
    cllick1: function() {
      let player = this.player;
      player.pause();
      player.src({
        type: "rtmp/mp4",
        src: "rtmp://184.72.239.149/vod/&mp4:BigBuckBunny_115k.mov"
      });
      player.ready(function() {
        player.load();
        player.play();
      });
    },
    cllick2: function() {
      let player = this.player;
      player.pause();
      player.src({
        type: "rtmp/mp4",
        src: "rtmp://119.254.111.185:6012/vodliverecord/Avengers2.mp4"
      });
      player.ready(function() {
        player.load();
        player.play();
      });
    },
    cllick3: function() {
      let player = this.player;
      player.pause();
      player.src({
        type: "rtmp/mp4",
        src: "rtmp://184.72.239.149/vod/&mp4:BigBuckBunny_115k.mov"
      });
      player.ready(function() {
        player.load();
        player.play();
      });
    },
    showClick: function() {-
      this.player.dispose()
      this.palyShow = !this.palyShow;
    }
  },
  mounted() {
    var thisp = this;
    let options = {
      //高度
      height: "360",
      //窗口自适应
      // fluid:true,
      playbackRates: [0.5, 1, 1.5, 2, 2.5],

      sources: [
        {
          type: "rtmp/mp4",

          src: "rtmp://pull-g.kktv8.com/livekktv/1009870384"
        }
      ],
      techOrder: ["flash"],
      autoplay: false,
      controls: false
      // poster:
      //   "https://surmon-china.github.io/vue-quill-editor/static/images/surmon-9.jpg"
    };
    var player = videojs("my-player", options);
    console.log(player);
    player.ready(function() {
      this.play();
    });
    player.on("ended", function() {
      console.log("视频播放完成");
    });
    player.on("pause", function() {
      console.log("视频暂停");
    });
    player.on("timeupdate", function() {
      var currentTime = this.currentTime();
      // console.log(thisp.progressLast, currentTime, "视频进度");
      // if (currentTime == thisp.progressLast && currentTime != 0) {
      //   player.pause();
      //   player.load();
      //   player.play();
      //   // player.ready(function() {
      //   //   player.load();
      //   //   player.play();
      //   // });
      // } else {
      //   thisp.progressLast = currentTime;
      // }
    });
        player.on("error", function() {
      console.log("视频加载错误");
    });
    player.on("waiting", function() {
      console.log("视频等待");
    });
    player.on("emptied", function() {
      console.log("媒体已经加载（或部分加载）");
    });
    this.player = player;

    var player1 = videojs("my-player1", options);
    console.log(player1);
    player1.ready(function() {
      this.play();
    });
    player1.on("ended", function() {
      console.log("视频播放完成");
    });
    player1.on("pause", function() {
      console.log("视频暂停");
    });
    this.player1 = player1;
  }
};
</script>

<style>
.visible {visibility:visible}
.invisible {visibility:hidden}
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
<style>
/* 暂停时显示播放按钮 */
.vjs-paused .vjs-big-play-button,
.vjs-paused.vjs-has-started .vjs-big-play-button {
  display: block;
}
/* 暂停按钮圆形 */
.video-js .vjs-big-play-button {
  font-size: 2.5em;
  line-height: 2.3em;
  height: 2.5em;
  width: 2.5em;
  -webkit-border-radius: 2.5em;
  -moz-border-radius: 2.5em;
  border-radius: 2.5em;
  background-color: #73859f;
  background-color: rgba(115, 133, 159, 0.5);
  border-width: 0.15em;
  margin-top: -1.25em;
  margin-left: -1.75em;
}
/* 中间的播放箭头 */
.vjs-big-play-button .vjs-icon-placeholder {
  font-size: 1.63em;
}
/* 加载圆圈 */
.vjs-loading-spinner {
  font-size: 2.5em;
  width: 2em;
  height: 2em;
  border-radius: 1em;
  margin-top: -1em;
  margin-left: -1.5em;
}
/* 进度显示当前播放时间 */
.video-js .vjs-time-control {
  display: block;
}
.video-js .vjs-remaining-time {
  display: none;
}
</style>

