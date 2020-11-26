<template>
  <div id="app"> 
  <TopNavigation/>
  <MainCanvas/>
  <LeftSidebar/>
  <RightSidebar/>
  </div>
</template>

<script>
import MainCanvas from '@/components/main-canva';
import TopNavigation from '@/components/top-navigation';
import LeftSidebar from '@/components/left-sidebar';
import RightSidebar from '@/components/right-sidebar';
export default {
  name: 'App',
  components: { MainCanvas, TopNavigation, LeftSidebar, RightSidebar },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
  overflow: hidden;
  background: radial-gradient( rgb(124, 125, 126), rgb(40, 40, 54));
  /* background: linear-gradient(180deg, rgb(46, 46, 66) 0%, rgb(129, 135, 136) 100%); */
}
</style>