<template>
  <!-- <link-text text="なんかurl" @on-click="clickUrl()" /> -->
  <div class=" m-2 bg-gray-400">
      <div class="h-48 bg-red-700">
          <button class="bg-gray-100" @click="RedirectToEditPage">作品を作成する</button>
      </div>
      <div class=" flex flex-row justify-center m-5 ">
        <CCard :title="Ccard_title" :imgsrc="require('@/static/apples.jpg')"/>
        <CCard :title="Ccard_title" :imgsrc="require('@/static/grapes.jpg')"/>
        <CCard :title="Ccard_title" :imgsrc="require('@/static/stroberries.jpg')"/>
      </div>
  </div>
</template>

<style scoped>


</style>

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
export default class index extends Vue {

  //propでは，特にプロップの値を取得するよ的な宣言はいらない．（prop自体が親のデータ領域に入っていると考えるとよい）
  Cbutton_text = "huga"

  Ccard_title = "hoge_title"


  count = 0;

  RedirectToEditPage(){
    return  this.$router.push('/edit');
  }

}
</script>
