<script setup>
// 引入标题图片组件
import HomePanel from './HomePanel.vue'
import {findNewAPI} from '@/apis/home'
import { onMounted,ref } from 'vue'


// 获取新鲜好物模块数据
const newList = ref([])
const getNewList = async() => {
    const res = await findNewAPI()
    newList.value = res.result
}
onMounted(() => getNewList())




</script>

<template>
  <!-- 1.HomePanel组件 新鲜好物模块-->
  <!-- Props -->
  <HomePanel title="新鲜好物" sub-title="新鲜好物 品质保证">
  <!-- 插槽 -->
    <ul class="goods-list">
    <li v-for="item in newList" :key="item.id">
      <RouterLink to="/">
        <img :src="item.picture" alt="" />
        <p class="name">{{ item.name }}</p>
        <p class="price">&yen;{{ item.price }}</p>
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