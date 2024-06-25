<script setup lang="ts">
useSeoMeta({
  title: '首页',
  description: '这是首页',
  keywords: '首页',
  referrer: 'no-referrer',
})
</script>
<template>
  <NuxtPage :keepalive="{ max: 10 }" />
</template>
<style lang="scss">
/* // 基础样式 */
@import './assets/styles/base.scss';
/* // 字体图标 */
@import './assets/styles/iconfont.scss';
/* vant-ui 主题定制 */
:root {
  --van-primary-color: #fb7299 !important;
  --van-back-top-background: #fbfbfb !important;
  --van-back-top-text-color: #666 !important;
}
</style>
