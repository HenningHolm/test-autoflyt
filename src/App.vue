<template>
  <div id="app"> 
  <TopNavigation/>
  <MainCanvas/>
  <LeftSidebar/>
  <RightSidebar/>
  </div>
</template>

<script>
import MainCanvas from '@/components/main-canvas';
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
}
</style>