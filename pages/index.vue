<template>
  <!-- <link-text text="なんかurl" @on-click="clickUrl()" /> -->
  <div class=" m-2 bg-gray-400">
      <div>

      </div>
      <div class=" flex flex-row ">
        <CCard :title="Ccard_title" :imgsrc="Ccard_imgsrc"/>
        <CCard :title="Ccard_title" :imgsrc="Ccard_imgsrc"/>
        <CCard :title="Ccard_title" :imgsrc="Ccard_imgsrc"/>
      </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "nuxt-property-decorator";


// @componentは，続けて定義しているクラスをVueが認識できる形式に変換する．
// つまり，クラスを後ろに必ず定義しないといけない．

//Dataは，クラス定義の中で利用する．
//computedはクラスのゲッターとして利用する．算出プロパティは，読み取り専用という意味．
//methodsはmethodsの中で利用する必要はなく，ただ関数としてかけばいいだけ．
 //pointは，getを付けないといけないのが，算出プロパティ(computed)で，getをつけなくていいのがmethods（関数）
 //@componentは，引数としてVueのオブジェクトを指定する


 
@Component
export default class ParentComponent extends Vue {

  //propでは，特にプロップの値を取得するよ的な宣言はいらない．（prop自体が親のデータ領域に入っていると考えるとよい）
  Cbutton_text = "huga"

  Ccard_title = "hoge_title"

  Ccard_imgsrc = require('@/static/img_product.jpg')

}
</script>
