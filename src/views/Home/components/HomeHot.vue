<script setup>
// 引入标题图片组件
import HomePanel from './HomePanel.vue'
import {getHotAPI} from '@/apis/home'
import { onMounted,ref } from 'vue'


// 获取人气推荐模块数据

const hotList = ref([])
const getHotList = async () => {
  const res = await getHotAPI()
  // 将res.result 赋值给 hotList.value
  hotList.value = res.result
  console.log(res)
}

onMounted(() => getHotList())


</script>

<template>
  <!-- 2.HomePanel组件 人气推荐模块-->
   <!-- Props -->
   <HomePanel title="人气推荐" sub-title="人气爆款 不容错过">
  <!-- 插槽 -->
    <ul class="goods-list">
        <li v-for="item in hotList" :key="item.id">
          <RouterLink to="/">
            <!-- 图片懒加载指令 -->
            <img v-img-lazy="item.picture" alt="">
            <p class="name">{{ item.title }}</p>
            <p class="desc">{{ item.alt }}</p>
          </RouterLink>
        </li>
      </ul>
  </HomePanel>
</template>


<style scoped lang='scss'>
.goods-list {
  display: flex;
  justify-content: space-between;
  height: 406px;

  li {
    width: 306px;
    height: 406px;

    background: #f0f9f4;
    transition: all .5s;

    &:hover {
      transform: translate3d(0, -3px, 0);
      box-shadow: 0 3px 8px rgb(0 0 0 / 20%);
    }

    img {
      width: 306px;
      height: 306px;
    }

    p {
      font-size: 22px;
      padding-top: 12px;
      text-align: center;
      text-overflow: ellipsis;
      overflow: hidden;
      white-space: nowrap;
    }

    .price {
      color: $priceColor;
    }
  }
}
</style>