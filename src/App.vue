<template>
  <div id="app">
    <!-- 头部 -->
    <app-header :poiInfo="poiInfo"></app-header>
    
    <!-- 导航 -->
    <app-nav></app-nav>

    <!-- 内容 -->
    <router-view></router-view>
  </div>
</template>

<script>
import Header from './components/header/header'
import Nav from './components/nav/nav'
export default {
  name: 'App',
  components: {
    'app-header': Header,
    'app-nav': Nav
  },
  data() {
    return {
      poiInfo: {}
    }
  },
  created() {
    fetch("/api/goods")
      .then(res => {
        return res.json()
      })
      .then(response => {
        if(response.code === 0) {
          this.poiInfo = response.data.poi_info
        }
      })
  }
}
</script>

<style>

</style>
