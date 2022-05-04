<template>
 <button class=".border-opacity-0 .border-current rounded-md bg-white border-4 pr-4 pl-4 w-full inline-block" >
    <!-- {{check_url_type}} -->
   {{text}}
 </button>
</template>

<style lang="css" scoped>

</style>

<script lang="ts">

import { Component, Prop, Vue } from "nuxt-property-decorator";

//propsは空箱のようなもの．親コンポーネントが，子供のpropsに値を渡す形になる
//slotはstringだけを渡す仕様．
//propsでは，オブジェクト構文として，実際に渡されているデータの種類が一致するかをチェックすることができる．
//

@Component
export default class CButton extends Vue {
  
  // 意味構文ではこの通りになる．
  // props: {
  //   hogetext: {
  //     type: String,
  //     require: true
  //   }
  // }

  @Prop({type: String, required: true, default:"any text"})
  //!は，required: trueのときに，デフォルトの値が設定されているプロパティにのみ指定する．NonNullAssertionオペレータと呼ばれる．
  //?はデフォルト値を指定していない場合に，undefinedの可能性があることを明示する．
  text?: string;

}
</script>
