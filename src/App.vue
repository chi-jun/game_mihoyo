<script setup>
import { RouterView } from 'vue-router'
</script>

<template>
  <router-view></router-view>
  <!-- <div id="app">
    
  </div> -->
</template>

<style>
  body {
    margin: 0;
    padding: 0;
  }
  #app {
    display: flex;
    justify-content: center;
  }

  ::-webkit-scrollbar {
    /*滚动条整体样式*/
    width: 4px; /*高宽分别对应横竖滚动条的尺寸*/
    height: 1px;
  }
  ::-webkit-scrollbar-thumb {
    /*滚动条里面小方块*/
    border-radius: 10px;
    box-shadow: inset 0 0 5px rgba(97, 184, 179, 0.1);
    background: #78b4b4;
  }
  ::-webkit-scrollbar-track {
    /*滚动条里面轨道*/
    box-shadow: inset 0 0 5px rgba(87, 175, 187, 0.1);
    border-radius: 10px;
    background: #ededed;
  }
  /* ::-webkit-scrollbar { width: 0 !important } */

</style>
