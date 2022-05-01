<template>
  
  <div>
    hoge
    <!-- <p @click="onClick">{{ text }}</p> -->
  </div> 
</template>

<script lang="ts">
import { Component, Emit, Prop, Vue } from "nuxt-property-decorator";

@Component({
  name: "Button",
})
export default class Button extends Vue {
  @Prop() private readonly text!: string;
  @Emit() private onClick(): void {}
}
</script>