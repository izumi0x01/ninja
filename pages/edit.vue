<template>
  
  <div id="container">
    
    <div class=" border-r-2 " id="left-sidebar">
      <CButton :text="home_button_text"  @click="$router.push('/')" />
    </div>
    <div id="drawarea" >
      <div  class=" w-80 h-80  border-2 border-black">
        <canvas  id="canvas_area"></canvas>
      </div>
    </div>
    <div class=" border-l-2 " id="right-sidebar">
      <CButton :text="save_button_text" @click="addWork"/>
    </div>
    <div class=" border-t-2 " id="toolbar">
      ここには，toolが置かれます．
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
    align-self: center;
    justify-self: center;
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
  import { Context } from "@nuxt/types";
  import { Container } from "postcss";
  import { fabric } from "fabric";


@Component({
  name: "edit",
})
export default class edit extends Vue {
  
  home_button_text = "一覧ページへ"
  save_button_text = "作品を保存"


  canvas?: fabric.Canvas;


  mounted()
  {
    this.canvas = new fabric.Canvas("canvas_area");
    this.canvas.isDrawingMode = true;
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
    const userRef = firestore.collection(userID).doc();
    var recordID = ""
    await userRef.set({
        title: "sample_title",
        created_at: "2022-05-06T12:00:00+0000",
        updated_at: "2022-05-06T13:00:00+0000",
        imageURL: ""
    }).then(() => {
      recordID = userRef.id
      console.log("recordID is: " + recordID);
    })

    //ファイルアップロードはblob⇔fileとして受け付けるっぽい．
    const canvas = <HTMLCanvasElement>document.getElementById('canvas_area');
    var canvasBlob: any = new Blob();
    
    canvasBlob =  await new Promise((resolve, reject) => {
      canvas.toBlob(function(Blob){resolve(Blob);},'image/png' );
    })

    // canvasBlobfunc.then((Blob : Blob) => {
    //   canvasBlob = Blob;
    //   console.log("blob data is: " + canvasBlob);
    //  // console.log("to change for blob is failed: " + error);
    // })

    console.log("blob data is: " + canvasBlob);
    
    //
    const storage = firebase.storage();
    const storageRef = storage.ref().child(userID);
    try{
      const imgname = recordID + '.png'
      const uploadTask = storageRef.child(imgname).put(canvasBlob);
      await uploadTask.on('state_changed',  (snapshot) => {
        // Observe state change events such as progress, pause, and resume
        // Get task progress, including the number of bytes uploaded and the total number of bytes to be uploaded
        var progress = (snapshot.bytesTransferred / snapshot.totalBytes) * 100;
        console.log('Upload is ' + progress + '% done');
        switch (snapshot.state) {
          case firebase.storage.TaskState.PAUSED: // or 'paused'
            console.log('Upload is paused');
            break;
          case firebase.storage.TaskState.RUNNING: // or 'running'
            console.log('Upload is running');
            break;
        }
      },
      (error) => {
        // Handle unsuccessful uploads
        console.log('firebase_upload中のエラー:' + error);
      },
      () => {
        uploadTask.snapshot.ref.getDownloadURL().then((downloadURL) => {
          console.log('File available at', downloadURL);

          //ここの書き方めっちゃ汚いのどうにかしたい．
          userRef.update({
            imageURL: downloadURL
          });
        });
      });
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