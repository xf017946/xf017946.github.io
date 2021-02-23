<template>
  <div class="home">
    <van-swipe ref="swiper" :show-indicators="false" @change="onChange">
      <van-swipe-item v-for="item of goodsData" :key="item.imgUrl">
        <div class="wrap-swiper-item">
          <img class="goods" :src="item.imgUrl" alt="">
          <p class="desc">{{ item.desc}}</p>
          <p class="price">{{ item.price ? `￥${item.price}`: '' }}</p>
        </div>
      </van-swipe-item>
    </van-swipe>
    <div>
      <p class="label">款式</p>
      <div class="wrap-labels">
        <span 
          v-for="(item, index) of goodsData"
          :key="item.name" :class="[{active: index === current}, 'labels']"
          @click="change(index)"
        >{{ item.name }}</span>
      </div>
    </div>
  </div>
</template>

<script>

import { ref } from 'vue'
export default {
  name: 'Home',
  setup() {
    const current = ref(0)
    const onChange = (index) => {
      current.value = index;
    }
    return {
      goodsData: [
        {
          imgUrl: require('../assets/1.jpeg'),
          name: '汽车名称1xx',
          price: '10',
          desc: '这是汽车名称1xx'
        },
        {
          imgUrl: require('../assets/2.jpeg'),
          name: '汽车名称2xx',
          price: '20元',
          desc: '这是汽车名称2xx'
        }
      ],
      current,
      onChange
    };
  },
  methods: {
    change(index){
      if (index !== this.current) {
        this.$refs.swiper.swipeTo(index);
      }
    }
  }
}
</script>

<style lang="scss" scoped>
  * {
    padding: 0;
    margin: 0;
  }
  .label {
    margin-left: 10px;
    text-align: left;
  }
  .wrap-labels {
    display: flex;
    justify-content: flex-start;
    margin: 10px 10px;
  }
  .labels {
    display: inline-block;
    padding: 2px 4px;
    margin-right: 8px;
    background: #efefef;
    border-radius: 4px;
    color: #000;
    &.active {
      color: #fff;
      background: #e80a0a;
    }
  }
  .goods {
    width: 100%;
    height: 280px;
    object-fit: cover;
  }
  .wrap-swiper-item {
    font-size: 0;
    position: relative;
    .desc {
      font-size: 14px;
      position: absolute;
      left: 0;
      right: 0;
      bottom: 20px;
      color: #fff;
      text-align: left;
      padding-left: 10px;
      background: rgba(0,0,0,0.3);
      line-height: 20px;
    }
    .price {
      font-size: 14px;
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      line-height: 20px;
      color: #ff7676;
      text-align: left;
      padding-left: 10px;
      background: rgba(0,0,0,0.3);
    }
  }
</style>