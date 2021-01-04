<template>
  <div id="app">
<!--    <div class="loading" v-show="$parent.isShowLoading">
		
		<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="24px" height="30px" viewBox="0 0 24 30" style="enable-background:new 0 0 50 50" xml:space="preserve">
			<rect x="0" y="9.22656" width="4" height="12.5469" fill="#d43c33">
				<animate attributeName="height" attributeType="XML" values="5;21;5" begin="0s" dur="0.6s" repeatCount="indefinite"></animate>
				<animate attributeName="y" attributeType="XML" values="13; 5; 13" begin="0s" dur="0.6s" repeatCount="indefinite"></animate>
			</rect>
			<rect x="10" y="5.22656" width="4" height="20.5469" fill="#d43c33">
				<animate attributeName="height" attributeType="XML" values="5;21;5" begin="0.15s" dur="0.6s" repeatCount="indefinite"></animate>
				<animate attributeName="y" attributeType="XML" values="13; 5; 13" begin="0.15s" dur="0.6s" repeatCount="indefinite"></animate>
			</rect>
			<rect x="20" y="8.77344" width="4" height="13.4531" fill="#d43c33">
				<animate attributeName="height" attributeType="XML" values="5;21;5" begin="0.3s" dur="0.6s" repeatCount="indefinite"></animate>
				<animate attributeName="y" attributeType="XML" values="13; 5; 13" begin="0.3s" dur="0.6s" repeatCount="indefinite"></animate>
			</rect>
		</svg>
      
		<span>正在加载中</span>
    </div> -->

    <Play
      v-if="currentMusic"
      :currentMusic="currentMusic"
      :playlist="playlist"
      :currentIndex="currentIndex"
      @update:paused="paused = $event"
      @update:music="
        currentMusic = $event.item;
        currentIndex = $event.index;
      "
    />

    <HomeNav v-if="$route.meta.isShowNav" />

    <keep-alive>
      <router-view
        @update:music="
          currentMusic = $event.item;
          currentIndex = $event.index;
        "
        @update:playlist="playlist = $event"
        v-bind:currentMusic="currentMusic"
        v-bind:paused="paused"
      />
    </keep-alive>
  </div>
</template>

<script>
import HomeNav from "@/components/HomeNav.vue";
import Play from "@/components/Play.vue";
export default {
  components: {
    HomeNav,
    Play,
  },
  data: function () {
    return {
      currentMusic: null,
      paused: null,
      playlist: [],
      currentIndex: 0,
    };
  },
  created() {
    console.log(this.$parent);
  },

};
</script>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

:root {
  --animate-duration: 300ms;
}

// .loading {
//   width: 100%;
//   height: 100vh;
//   position: fixed;
//   top: 0;
//   left: 0;
//   z-index: 999;
//   display: flex;
//   justify-content: center;
//   align-items: center;
//   svg {
//     animation: loading 3s linear infinite;
// 	font-size: 12px;
//   }
//   span{
// 	padding-left: 10px;
// 	font-size: 12px;
// 	color: #888;
//   }
// }
// @keyframes loading {
//   from {
//     transform: rotate(0deg);
//   }
//   to {
//     transform: rotate(360deg);
//   }
// }
</style>
