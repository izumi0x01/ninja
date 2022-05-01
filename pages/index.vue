<template>
  <link-text text="なんかurl" @on-click="clickUrl()" />
</template>

<script lang="ts">
import { Component, Prop, Vue } from "nuxt-property-decorator";

import Button from "../components/Button.vue";


// @componentは，続けて定義しているクラスをVueが認識できる形式に変換する．
// つまり，クラスを後ろに必ず定義しないといけない．

//Dataは，クラス定義の中で利用する．
//computedはクラスのゲッターとして利用する．算出プロパティは，読み取り専用という意味．
//methodsはmethodsの中で利用する必要はなく，ただ関数としてかけばいいだけ．
 //pointは，getを付けないといけないのが，算出プロパティ(computed)で，getをつけなくていいのがmethods（関数）
 //@componentは，引数としてVueのオブジェクトを指定する
 
@Component({
  name: "ParentComponent",
  components: {
    Button,
  }
})
export default class ParentComponent extends Vue {
  private clickUrl(): void {
    // なんかクリックされたときの処理
  }
  message = ""
  async mounted(){
    let res = await firebase.functions().httpsCallable('helloWorld')();
    this.message = res.data.message;
 }
}
</script>
