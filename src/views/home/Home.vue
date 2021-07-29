<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">欢迎光临</div></nav-bar>
    <home-swiper :banners="banners"></home-swiper>
    <home-recommend-view :recommends="recommends"></home-recommend-view>
  </div>
</template>

<script>
  import NavBar from "../../components/common/navbar/NavBar";
  import HomeSwiper from "./childComps/HomeSwiper";
  import HomeRecommendView from "./childComps/HomeRecommendView";

  import {getHomeMultidata} from "../../network/home";

  /*import {Swiper, SwiperItem} from "../../components/common/swiper"*/

  export default {
    name: "Home",
    components: {
      NavBar,
      HomeSwiper,
      HomeRecommendView
    },
    data() {
      return {
        //数据保存
        banners: [],
        recommends: []
      }
    },
    created() {
      //1、请求多个数据
      getHomeMultidata().then(res => {
        console.log(res);
        //保存请求的数据
        //获取data下的banner.list
        this.banners = res.data.banner.list
        this.recommends = res.data.recommend.list

      })
    }
  }
</script>

<style >
  .home-nav {
    background-color: var(--color-tint);
    color: white;
  }
</style>
