<template>
  <div class="booksViewer" @click="showNavigation=!showNavigation">
    <div ref="nav" class="page_navigation" :style="{ display: showNavigation == true ? 'block' : 'none'}">
      <span class="page_navigation-close" @click="backToSeries">X</span>{{ booksData.title }}
    </div>
    <carousel :per-page="1" :navigation-enabled="false" :paginationEnabled="false" :navigateTo="[preIndex,false]" @pageChange="onPageChange">
      <slide>
        <div class="slide_wrapper">
          <div>
            最後のページです！
          </div>
          <div class="slide_btn" @click="backToSeries">
            一覧に戻る
          </div>
        </div>
      </slide>
      <template v-for="(element, index) in booksData.imageData">
        <slide :key="index" class="slide_page">
          <template>
            <v-lazy-image :src="`${element.imageUrl}`"/>
          </template>
        </slide>
      </template>
      <slide>
        <div class="slide_wrapper">
          <div class="title">
            {{ booksData.title}}
          </div>
          <div class="pageNum">
            総ページ数：{{ booksData.pageNum }}
          </div>
          <div class="slide_info">
            ＜ 横にスライドでめくる
          </div>
        </div>
      </slide>
    </carousel>
    <div class="nowPageBanner">
      {{ -preIndex + (booksData.pageNum + 2) }} / {{ booksData.pageNum + 2}}
    </div>
  </div>
</template>
<script>
import axios from 'axios'

export default {
  data() {
    return {
      showNavigation: true,
      preIndex: 0
    }
  },
  async asyncData({ params }) {
    const myHttpClient = axios.create({
      baseURL: "https://wfc2-image-api-259809.appspot.com/api/"
    })
    var data = await Promise.all([
      myHttpClient.get('books/' + params.id)
    ])
    return { booksData: data[0].data,preIndex: (data[0].data.pageNum + 1)};
  },
  mounted() {
    this.reverseData()
    setTimeout(this.deleteNav, 3000);
  },
  methods: {
    deleteNav() {
      this.showNavigation = false;
    },
    reverseData() {
      this.booksData.imageData = this.booksData.imageData.slice(0).reverse();
      console.log(this.booksData);
    },
    onPageChange(index) {
      console.log("waduhaowuidho" + index);
      this.preIndex = index;
    },
    backToSeries() {
      console.log(this.booksData.seriesId);
      this.$router.push({ path: `/series/${this.booksData.seriesId}` });
    }
  }
}

</script>
<style scoped>
.v-lazy-image {
  opacity: 0;
  transition: opacity .4s;
}
.v-lazy-image-loaded {
  opacity: 1;
}
.page_navigation {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 58px;
  background-color: #0F4C81;
  z-index: 99999;
  color: white;
  vertical-align: middle;
  /* 「vertical-align」を指定してもテキストは縦方向中央揃いにならない */
  text-align: center;
  line-height: 58px;
}

.page_navigation-close {
  padding: 16px;
}

.slide_wrapper {
  width: 100vw;
  height: 100%;
  display: flex;
  /* 子要素をflexboxで揃える */
  flex-direction: column;
  /* 子要素をflexboxにより縦方向に揃える */
  justify-content: center;
  /* 子要素をflexboxにより中央に配置する */
  align-items: center;
  /* 子要素をflexboxにより中央に配置する */
  border: 16px solid;
}

.slide_page>img {
  width: 100vw;
  height: 100vh;
  object-fit: contain;
}

.slide_info {
  margin-top: 20px;
  animation-name: fade;
  animation-duration: 5s;
  animation-timing-function: ease;
  animation-iteration-count: infinite;
}

.slide_btn {
  background-color: #0F4C81;
  color: white;
  margin: 16px;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 16px;
  padding-right: 16px;
  border-radius: 5px;
}

.nowPageBanner {
  position: absolute;
  bottom: 16px;
  left: 0;
  right: 0;
  margin: auto auto;
  background-color: rgba(0, 0, 0, 0.4);
  padding: 5px;
  width: 50px;
  border-radius: 5px;
}

@keyframes fade {
  0% {
    color: rgba(0, 0, 0, 0.1);
  }

  50% {
    color: rgba(0, 0, 0, 0.8);
  }

  100% {
    color: rgba(0, 0, 0, 0.1);
  }
}

</style>
