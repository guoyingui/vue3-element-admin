<template>
  <div class="app-main">
    <h2>app main</h2>
    <!-- vue3 路由缓存 https://next.router.vuejs.org/guide/migration/index.html#router-view-keep-alive-and-transition -->
    <router-view v-slot={Component}>
      <transition name="fade-transform" mode="out-in">
        <keep-alive :include="cachedViews">
          <component :is="Component" />
        </keep-alive>
      </transition>
    </router-view>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent } from 'vue'
import { useStore } from '@/store'

export default defineComponent({
  name: 'AppMain',
  setup() {
    const store = useStore()
    const cachedViews = computed(() => store.state.tagsView.cachedViews)
    return {
      cachedViews
    }
  }
})
</script>

<style lang="scss" scoped>
.app-main {
  /* 50= navbar  50  如果有tagsview + 34  */
  min-height: calc(100vh - 84px);
  background: red;
}

.fade-transform-enter-active,
.fade-transform-leave-active {
  transition: all .5s;
}

.fade-transform-enter-from {
  opacity: 0;
  transform: translateX(-30px);
}

.fade-transform-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>
