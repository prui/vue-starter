<template>
<div>
  <!-- <mt-header fixed :title="title">
    <router-link to="/home" slot="left">
      <mt-button icon="back">返回</mt-button>
    </router-link>
  </mt-header> -->

  <navBar></navBar>

  <transition :name="transitionName" mode="out-in">
    <keep-alive>
    <router-view class="child-view"></router-view>
    <keep-alive>
  </transition>
</div>
</template>

<script>
import navBar from '../components/navBar';
export default {
  name: 'app',
  data() {
    return {
      transitionName: 'slide-left'
    };
  },
  computed: {
    title() {
      return this.$store.state.title;
    }
  },
  components: {
    navBar
  },
  watch: {
    $route: function(to, from) {
      // const toDepth = to.path.split('/').length;
      // const fromDepth = from.path.split('/').length;
      this.transitionName = from.meta.backRouter === to.name ? 'slide-right' : 'slide-left';
      // console.log(this.transitionName);
    }
  },
  methods: {
    // startHacking() {
    //   this.$toast('It Works!');
    // }
  }
};
</script>

<style lang="scss">
* {
    margin: 0;
}

body,
html {
    height: 100%;
    width: 100%;
}

.mobile_app {
    height: 100%;
}

.app_content {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    height: 100%;
    overflow-y: auto;
    -webkit-overflow-scrolling: touch;
}
.mobile_app_view {
    height: 100%;
}

.has_title {
    top: 40px;
    position: relative;
    height: calc(100% - 40px);
}

.header_bar {
    width: 100%;
    background-color: #26a2ff;
    height: 40px;
    position: fixed;
    top: 0;
}

.child-view {
    transition: all 0.3s cubic-bezier(0,1,.4,1);
    height: 100%;
}

.slide-left-enter,
.slide-right-leave-active {
    opacity: 0.25;
    -webkit-transform: translate(100%, 0);
    transform: translate(100%, 0);
}
.slide-left-leave-active,
.slide-right-enter {
    opacity: 0.25;
    -webkit-transform: translate(-100%, 0);
    transform: translate(-100%, 0);
}
</style>
