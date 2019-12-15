<template>
  <div class="lib">
    保存ボタン押したら
    fetch
    blob
    保存する
    保存されてたら
    url.createObjectUrl
    ソースに入れる
    revokeObjectURL
    <div v-if="downloadRequestBookData != null && downloadRequestBookData != undefined">
      {{downloadRequestBookData}}
    </div>
    <div v-if="preview">
      <img :src="preview">
    </div>
  </div>
</template>
<script>
import * as localforage from 'localforage';
import axios from 'axios'
export default {
  data: function() {
    return {
      downloadRequestBookData: null,
      preview: ""
    }
  },
  mounted: function() {
    this.isSave();
  },
  methods: {
    async isSave() {
      var querys = this.$route.query.downloadBookId;
      var drbd = null;
      if (querys != undefined && querys != null) {
        console.log(querys);
        const myHttpClient = axios.create({
          baseURL: "https://wfc2-image-api-259809.appspot.com/api/"
        })
        var data = await Promise.all([
          myHttpClient.get('books/' + this.$route.query.downloadBookId)
        ])
        drbd = data;
      } else {
        console.log("くえりーにはなにもないので");
      }
      this.downloadRequestBookData = drbd;
      this.downloadBook(drbd);
    },
    downloadBook(drbd) {
      var nowItem = localStorage.getItem("library");
      if (nowItem != null) {
        var newItem = JSON.parse(nowItem);
        var found = newItem.find(ele => ele.data.seriesId == drbd[0].data.seriesId);
        if (found === undefined) {
          var currentItem = drbd;
          newItem.push(currentItem);
        }
        localStorage.setItem("library", JSON.stringify(newItem));
      } else {
        var newItem = [JSON.stringify(drbd)];
        localStorage.setItem("library", newItem)
      }

      this.chengeUrl();
    },
    chengeUrl() {
      var nowItem = localStorage.getItem("library");
      console.log("widhaowidhoaw");
      nowItem = JSON.parse(nowItem);
      console.log(nowItem);
      nowItem = nowItem[0].data;
      for (var i = 0; i < nowItem.imageData.length; i++) {
        var imageUrl = nowItem.imageData[i].imageUrl;
        imageUrl = imageUrl.slice(8);
        imageUrl = "https://cdn.statically.io/img/" + imageUrl;
        nowItem.imageData[i].imageUrl = imageUrl;
        axios.get(imageUrl)
          .then(response => {
            var blob = new Blob([response.data], { type: "image/png", });
            var objectURL = URL.createObjectURL(blob);
            console.log("objectURL");
            console.log(objectURL);
            this.preview = objectURL;
          })
          .catch(response => {
            console.log(response)
          })
      }
      console.log("result");
      console.log(nowItem);

    }
  }
}

</script>
<style>
</style>
