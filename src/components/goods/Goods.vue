<template>
  <div class="goods">
    <!-- 分类列表 -->
    <div class="menu-wrapper">
      <ul>
        <!-- 专场 -->
        <li class="menu-item">
          <p class="text">
            <img  class="icon" :src="container.tag_icon" v-if="container.tag_icon">
            {{container.tag_name}}
          </p>
        </li>
        <li class="menu-item" v-for="(item, index) in goods" :key="index">
          <p class="text">
            <img class="icon" :src="item.icon" v-if="item.icon">
            {{item.name}}
          </p>
        </li>
      </ul>
    </div>
    <!-- 商品列表 -->
    <div class="foods-wrapper">
      <ul>
        <!-- 专场 -->
        <li class="container-list">
          <div v-for="(item, index) in container.operation_source_list" :key="index">
            <img :src="item.pic_url">
          </div>
        </li>
        <!-- 具体分类 -->
        <li class="food-list" v-for="(item, index) in goods" :key="index">
          <h3 class="title">{{item.name}}</h3>
          <!-- 具体商品列表 -->
          <ul>
            <li v-for="(food, index) in item.spus" :ksy="index">
              <div class="icon" :style="head_bg(food.picture)"></div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      container: {},
      goods:[]
    }
  },
  // 计算属性不能接受参数
  methods:{
    head_bg(imgName) {
      return 'background-image:url(' + imgName + ')'
    }
  },
  created() {
    fetch("/api/goods")
      .then(res => {
        return res.json()
      })
      .then(response => {
        if(response.code === 0) {
          this.container = response.data.container_operation_source
          this.goods = response.data.food_spu_tags
        }
        console.log(this.container);
        console.log(this.goods);
      })
  }
}
</script>
<style scoped>
.goods {
  display: flex;
  position: absolute;
  top: 190px;
  bottom: 50px;
  overflow: hidden;
  width: 100%;
}
.goods .menu-wrapper {
  flex: 0 0 85px;
  background: #f4f4f4;
}
.goods .foods-wrapper {
  flex: 1;
  background: #ff0;
}
/* Menu item */
.goods .menu-wrapper .menu-item {
  padding: 16px 23px 15px 10px;
  border-bottom: 1px solid #e4e4e4;
}
.goods .menu-wrapper .menu-item .text {
   font-size: 13px;
   color: #333;
   line-height: 17px;
   vertical-align: middle;
   -webkit-line-clamp:2;
   display: -webkit-box;
   -webkit-box-orient: vertical;
   overflow: hidden;
}
.goods .menu-wrapper .menu-item .text .icon {
  width: 15px;
  height: 15px;
  vertical-align: middle;
}
</style>
