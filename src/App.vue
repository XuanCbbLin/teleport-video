<template>
  <!-- 離開主影片的小播放區塊 -->
  <div id="small" v-show="isSmallVideo"></div>

  <!-- 主影片播放區 -->
  <div class="main-video" ref="mainTarget">
    <Teleport to="#small" :disabled="mainVideoDisabled">
      <div id="main-video"></div>
    </Teleport>
  </div>

  <div class="scroll"></div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useIntersectionObserver } from "@vueuse/core";
import Player from "xgplayer/dist/simple_player";

const mainTarget = ref(null);
const mainVideoDisabled = ref(true);
const isSmallVideo = ref(false);

onMounted(() => {
  const player = new Player({
    id: "main-video",
    url: "//sf1-cdn-tos.huoshanstatic.com/obj/media-fe/xgplayer_doc_video/mp4/xgplayer-demo-720p.mp4",
    poster: "//lf9-cdn-tos.bytecdntp.com/cdn/expire-1-M/byted-player-videos/1.0.0/poster.jpg",
    width: "100%",
    height: "100%",
  });

  // 判斷主影片播放區是否還在viewport
  useIntersectionObserver(mainTarget, ([{ isIntersecting }]) => {
    mainVideoDisabled.value = isIntersecting;
    isSmallVideo.value = !mainVideoDisabled.value;
  });
});
</script>

<style lang="scss">
.main-video {
  width: 1200px;
  height: 700px;
}

#small {
  width: 300px;
  height: 150px;
  border: 1px solid black;
  position: fixed;
  right: 10px;
  bottom: 10px;
}

.scroll {
  height: 1800px;
}
</style>
