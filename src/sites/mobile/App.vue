<template>
  <div v-if="title != '/'" id="nav">{{ title }}</div>
  <router-view />
</template>
<script lang="ts">
import { defineComponent, ref, watch } from 'vue';
import { useRoute } from 'vue-router';
import { isMobile } from '@/sites/assets/util';
export default defineComponent({
  name: 'app',
  components: {},
  setup() {
    const title = ref('NutUI');
    // 获取当前路由
    const route = useRoute();
    // 当当前路由发生变化时，调用回调函数
    watch(
      () => route,
      () => {
        // const { origin, hash, pathname } = window.top.location;
        const { hash } = window.top.location;
        if (!isMobile && route.hash != hash) {
          // window.top.location.replace(`${origin}${pathname}#/${route.hash}`);
          title.value = route.name as string;
        } else {
          title.value = route.name as string;
        }
      },
      {
        immediate: true,
        deep: true
      }
    );

    return { title };
  }
});
</script>

<style lang="scss">
#app {
  font-family: PingFangSC-Regular;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -webkit-text-size-adjust: none;
  -ms-text-size-adjust: 100%;
  background: #fff;
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;

  #nav {
    position: fixed;
    z-index: 10;
    left: 0;
    right: 0;
    height: 57px;
    line-height: 57px;
    text-align: center;
    background: $white;
    font-weight: bold;
    font-size: 20px;
    color: rgba(51, 51, 51, 1);
    box-shadow: 0px 4px 10px 0px rgba(0, 0, 0, 0.07);
  }

  .demo {
    height: 100%;
    background: #f7f8fa;
    overflow-x: hidden;
    overflow-y: auto;
    padding: 57px 25px 0 25px;

    &.full {
      padding: 57px 0 0 0;
      h2 {
        padding-left: 25px;
      }
    }

    &.bg-w {
      background: #fff;
    }

    &::-webkit-scrollbar {
      width: 0;
      background: transparent;
    }
    > h2 {
      height: 56px;
      line-height: 56px;
      font-size: 14px;
      color: rgba(144, 156, 164, 1);
    }

    .card {
      padding: 25px 18px;
      background: rgba(255, 255, 255, 1);
    }
  }
}
</style>
