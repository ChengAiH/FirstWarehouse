<template>
  <div class="home">
    <div id="nav">
      <router-link to="/home">推荐音乐</router-link> |
      <router-link to="/home/hot">热歌榜</router-link>
      <router-link to="/home/search">搜索</router-link>
    </div>


    <router-view></router-view>
  </div>
</template>

<script>

export default {
  name: "Home",
};
</script>
