<template>
  <div class="index" v-scroll="onScroll">
    <sidebar :isShowSidebar="isShowSidebar" v-on:hideSidebar="toggleSidebar"></sidebar>
    <mt-loadmore :top-method="loadTop" :topDistance="40" ref="loadmore">
      <header>
        <i class="icon iconfont icon-fenlei" @click="toggleSidebar"></i>
        <span class="hot-news">今日热闻</span>
      </header>
      <swipe></swipe>
      <newsList ref="newsList"></newsList>
    </mt-loadmore>
  </div>
</template>
<script>
import Swipe from '../components/Swipe';
import NewsList from '../components/NewsList';
import Sidebar from '../components/Sidebar';

export default {
  data() {
    return {
      isShowSidebar: false
    };
  },
  created() {
    this.isShowSidebar = false;
  },
  components: {
    'swipe': Swipe,
    'newsList': NewsList,
    'sidebar': Sidebar
  },
  methods: {
    // 切换侧边栏显示状态
    toggleSidebar() {
      this.isShowSidebar = !this.isShowSidebar;
    },
    // 下拉刷新数据
    loadTop() {
      this.$refs.newsList.$emit('refresh');
      this.$refs.loadmore.onTopLoaded();
    },
    onScroll(e, position) {
      console.log(position);
    }
  }
};
</script>
<style lang="sass" scoped>
@import "../assets/sass/pages/Index.sass";
</style>
