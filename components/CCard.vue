<template>
  <div class=".border-opacity-0 .border-current rounded-md bg-white border-4 "  >
    <!-- {{check_url_type}} -->

    <!-- nuxt-img では，urlが効かない -->
      <div id="container">
          <img  class="h-40 p-2 m-4 .border-2 bg-gray-50" id="picture_area" :src="imgsrc" />
          <div class=".self-center " id="title_area">
            題名：{{title}}
          </div>
          <ul class=".self-center " id="info_area"> 
            <li >
              製作日：{{title}}
            </li>
            <li>
              更新日：{{title}}
            </li>
          </ul>
          <CButton :text="Cbutton_text" id="button_area"/>
      </div>
  </div>
</template>

<style lang="css" scoped>

  #container{
    font-size: 62.5%;
    display: grid;
    justify-items: center;
    align-items: center;
    grid-template-rows: auto 5em 4em 8em;
    grid-template-columns: auto;
  }

  #picture_area{
    grid-row: 1/2;
  }

  #title_area{
    font-size: 2em; 
    grid-row: 2/3;
  }

  #info_area{
    font-size: 1.4em; 
    grid-row: 3/4;

  }

  #button_area{
    grid-row: 4/5;
  }
</style>

<script lang="ts">

import { Component, Prop, Vue } from "nuxt-property-decorator";

//propsは空箱のようなもの．親コンポーネントが，子供のpropsに値を渡す形になる
//slotはstringだけを渡す仕様．
//propsでは，オブジェクト構文として，実際に渡されているデータの種類が一致するかをチェックすることができる．
//

@Component
export default class Ccard  extends Vue {
  
  // 意味構文ではこの通りになる．
  // props: {
  //   hogetext: {
  //     type: String,
  //     require: true
  //   }
  // }

  // get check_url_type(){
  //   return typeof this.imgsrc;
  // }

  Cbutton_text = "edit"

  @Prop({type: String, required: true, default:"any text"})
  //!は，required: trueのときに，デフォルトの値が設定されているプロパティにのみ指定する．NonNullAssertionオペレータと呼ばれる．
  //?はデフォルト値を指定していない場合に，undefinedの可能性があることを明示する．
  title?: string;

  @Prop({type: String, required:true, default:require('@/static/img_product.jpg')})
  imgsrc?: string;

  //nuxtで日付をどうやって扱うか
  // @Prop({type: Date, required: true, default:"any text"})
  // //!は，required: trueのときに，デフォルトの値が設定されているプロパティにのみ指定する．NonNullAssertionオペレータと呼ばれる．
  // //?はデフォルト値を指定していない場合に，undefinedの可能性があることを明示する．
  // updated_time?: date;


}
</script>
