<template>
  
  <div id="container">
    
    <div class=" border-r-2 " id="left-sidebar">
      hoge
    </div>
    <div id="drawarea">
      hugahuga
    </div>
    <div class=" border-l-2 " id="right-sidebar">
      hoge
    </div>
    <div class=" border-t-2 " id="toolbar">

    </div>
  </div>

</template>

<style lang="css" scoped>

    #container{
      width: 100vw;
      height: 100vh;
    /* font-size: 62.5%; */
    display: grid;
    grid-template-rows: 70% 30%;
    grid-template-columns: 240px auto 240px;

    /* 1xl: '48px', lg: '24px'*/
  }

  #left_sidebar{
    grid-row: 1/2;
    grid-column: 1/2;
  }

  #drawarea{
    grid-row: 1/2;
    grid-column: 2/3;
  }

  #right_sidebar{
    grid-row: 1/2;
    grid-column: 3/4;

  }

  #toolbar{
    grid-row: 2/3;
    grid-column: 1/4;
    background-color: gray;
  }

</style>

<script lang="ts">

import { Component, Prop, Vue } from "nuxt-property-decorator";
export default class edit extends Vue {

}
</script>