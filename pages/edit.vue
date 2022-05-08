<template>
  
  <div id="container">
    
    <div class=" border-r-2 " id="left-sidebar">
      <CButton :text="home_button_text"  @click="$router.push('/')" />
    </div>
    <div id="drawarea">
        <canvas id="canvas_area">
        </canvas >
    </div>
    <div class=" border-l-2 " id="right-sidebar">
      <CButton :text="一覧ページへ" @click="set_works_to_db"/>
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
  import "firebase/firestore";
  import firebase from "firebase/app";
  import "firebase/storage";


@Component({
  name: "edit",
})
export default class edit extends Vue {
  
  home_button_text = "一覧ページへ"
  save_button_text = "作品を保存"

  //今は仮段階なので，遷移後に何もデータがないのはさみしい．
  mounted()
  {
    var canvas = <HTMLCanvasElement>document.getElementById('canvas_area');
    if (canvas.getContext) {

    var context = <CanvasRenderingContext2D>canvas.getContext('2d');

    //左から20上から40の位置に、幅50高さ100の四角形を描く
    context.fillRect(20,40,50,100);

    //色を指定する
    context.strokeStyle = 'rgb(00,00,255)'; //枠線の色は青
    context.fillStyle = 'rgb(255,00,00)'; //塗りつぶしの色は赤

    //左から200上から80の位置に、幅100高さ50の四角の枠線を描く
    context.strokeRect(200,80,100,50);

    //左から150上から75の位置に、半径60の半円を反時計回り（左回り）で描く
    context.arc(150,75,60,Math.PI*1,Math.PI*2,true);
    context.fill();
    };
  }

  //async関数の書き方
  // 基本：async (変数：型) = { await 関数：(promiseが確定するまで待機) }

  addWork = async (userID: string) =>
  { 
    // firebase.firestore => columの生成｛title, 作成時間，更新時間｝，columのidの取得
    // CANVASをimageに変換し，imageに変換後にidの名前を付ける
    // firebase.storage => idの名前で画像を保存, 保存先のリンクを取得
    // firebase.firestore => カラムに画像のリンクを保存
    
    //
    const firestore = firebase.firestore();
    userID = "test_user" //sample.後で消される．
    const userRef = firestore.collection(userID);
    const columID = ""
    userRef.doc().set({
        title: "sample_title",
        created_at: "2022-05-06T12:00:00+0000",
        updated_at: "2022-05-06T13:00:00+0000",
        imageURL: ""
    })

    //ファイルアップロードはblob⇔fileとして受け付けるっぽい．
    const canvas = <HTMLCanvasElement>document.getElementById('canvas_area');
    var canvasBlob: any = new Blob();
    canvas.toBlob(
      function(Blob){canvasBlob = Blob;},
      'image/png'
    );

    //
    const storage = firebase.storage();
    const storageRef = storage.ref().child(userID);
    try{
      const uploadTask = storageRef.child('${columID}.png').put(canvasBlob);
    }catch(error)
    {
      console.log('firebase_uploadのエラー:' + error);
    }

    //

  }

  updateWork = async () =>
  {
    // firebase.firestore => columの取得
    // CANVASをimageに変換.
    // firebase.storage => firestoreに保存されている保存先のリンクを元に，firestoreにアクセス．
    // firebase.firestore => columの更新｛title, 更新時間｝
    


  }

  deleteWork = async() =>
  {

  }

  // async set_works_to_db()
  // {

  //       // まず，CANVASをBase64に変換
  //       var canvas = <HTMLCanvasElement>document.getElementById('canvas_area');
  //       var data = canvas.toDataURL("image/jpeg");

  //       //edit画面で，DBにファイルをアップロードする．
  //       // ここでアップロードされるのは，更新日時とtitleと画像そのもの．
  //       //viewer画面と，edit画面で，データをダウンロードする．
  //       // viewer画面では，データのtitleと，storeの画像のリンク先と，

  //       // asyncとは，非同期関数を定義する関数宣言のこと．        
  //       // awaitとは，async function内でpromiseの結果が返されるまで待機する．（resolve、reject）が返されるまで待機


  //       const handleUpload = async (accepterdImg: any) => {

  //       }

  //       const db = firebase.firestore();
  //       var work_unique_ID = "";

  //       //ユーザ固有IDに空のカラムを追加．
  //       var workRef = db.collection("users").doc();

  //       // IDを保存．
  //       work_unique_ID = workRef.id;

  //       //storageにアクセスする． 
  //       var storageRef = firebase.storage().ref();
  //       var mountainImagesRef = storageRef.child('users/' + (String)(storageRef) + '.jpg');

  //       //正規表現．^:行の先頭の文字列を検索 $:行の終わりの文字列を検索 [: ]: .:何でもよい一文字

  //       // imageは，user名/固有ID.jpgにする．
  //       // storageに，user名/固有ID.jpgを保存，

  //       // 画像の保存先のパスを取得．
        

  //       workRef.set({
  //           title: "sample_title",
  //           created_at: "2022-05-06T12:00:00+0000",
  //           updated_at: "2022-05-06T13:00:00+0000"

  //       })
  //       .catch((error) => {
  //           console.error("Error adding document: ", error);
  //       });
  // }


}
</script>