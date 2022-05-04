<template>
  
  <div id="container">
    <div id="left-sidebar">

    </div>
    <div id="drawarea">

    </div>
    <div id="right-sidebar">

    </div>
    <div id="toolbar">

    </div>
  </div>

</template>

<style lang="css" scoped>

    #container{
    max-width: 100%;
    max-height: 100%;
    /* font-size: 62.5%; */
    display: grid;
    grid-template-rows: 20% 80% 20%;
    grid-template-columns: 70% 30%;
  }

  #left_sidebar{
    grid-row: 1/2;
    grid-column: 1/2;
    background-color: blue;
  }

  #drawarea{
    grid-row: 1/2;
    grid-column: 2/3;
    background-color: red;
  }

  #right_sidebar{
    grid-row: 1/2;
    grid-column: 3/4;
    background-color: green;

  }

  #toolbar{
    grid-row: 1/2;
    grid-column: 1/4;
    background-color: pink;
  }

</style>

<script lang="ts">

import { Component, Prop, Vue } from "nuxt-property-decorator";
export default class edit extends Vue {

}
</script>