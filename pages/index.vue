<template>
  <!-- <link-text text="なんかurl" @on-click="clickUrl()" /> -->
  <div class=" m-2">
      <div class="h-48 bg-gray-50">
          <!-- <button class="bg-gray-100" @click="set_works_to_db_2">DB_send_test_2</button> -->
          <!-- <button class="bg-gray-100" @click="get_works_from_db"> get_works_from_db</button> -->
          <CButton :text="edit_button_text"  @click="$router.push('/edit')" />
      </div>
      <div class=" flex flex-row justify-center m-5 " v-for="(Work, index) in Works" :key="index">
        <CCard :title="Work.title" :imgsrc="Work.imageURL"  :updated_date="Work.updated_at" :created_date="Work.created_at"/>
      </div>
  </div>
</template>

<style scoped>


</style>

<script lang="ts">
  import { Component, Prop, Vue } from "nuxt-property-decorator";
  import "firebase/firestore";
  import firebase from "firebase/app";
  import "firebase/storage";

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
  edit_button_text = "作品を作る"
  Ccard_title = "hoge_title"

  Works : object[] = [];

  mounted()
  {
    this.getWorks();
  }


  getWorks()
  {
    const db = firebase.firestore();

    db.collection("test_user").get().then((snapshot) => {
      snapshot.forEach((doc) => {
        console.log(doc.data());
        this.Works.push(doc.data());
      })
    
    }).catch((error) => {
      console.error(error);
    });
  }

   set_works_to_db_2()
  {

    // 1, 画像？をfirebase_storageに保存.
    var storageRef = firebase.storage().ref();
    var userRef = storageRef.child('users');
    var DL_URL = "";


  }



  


}
</script>
