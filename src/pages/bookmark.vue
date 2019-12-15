<template>
  <div class="bookmark">
    <header class="color_white background_maincolor">
      <div class="global">
        <router-link class="search" to="/">X</router-link>
        <div class="title"></div>
        <div>&nbsp&nbsp&nbsp&nbsp</div>
      </div>
    </header>
    <div class="flexbox" v-if="bookData != null && bookData != undefined">
      保存したしおり
      <nuxt-link v-for="(element, index) in bookData" v-bind:to="`/bookViewer/${ bookmarks[index].books}?page=${bookmarks[index].page }`">
        <template>
          <v-lazy-image :src="`${element.data.imageData[bookmarks[index].page-2].imageUrl}`" />
        </template>
      </nuxt-link>
    </div>
  </div>
</template>
<script scoped>
import axios from 'axios';
export default {
  data() {
    return {
      bookmarks: null,
      bookData: null
    }
  },
  mounted() {
    this.getBookmarks();
  },
  methods: {
    async getBookmarks() {
      this.bookmarks = JSON.parse(localStorage.getItem("bookmark"));


      const myHttpClient = axios.create({
        baseURL: "https://wfc2-image-api-259809.appspot.com/api/"
      })
      var reqs = [];
      for (var i = 0; i < this.bookmarks.length; i++) {
        reqs.push(myHttpClient.get('books/' + this.bookmarks[i].books));
      }
      var data = await Promise.all(reqs)
      this.bookData = data;
    }
  }
}

</script>
<style scoped>
.flexbox {
  display: flex;
  flex-wrap: wrap;
  border: 1px solid #ddd;
  padding: 0.4em;
  margin: 0 0 2em;
  text-align: center;
}

.flexbox>a {
  background: #ddd;
  padding: 1em;
  flex: 1 0 calc(50vw - 2em);
  margin: 0.4em;
}

.flexbox>a>img {
  width: 200px;
  max-width: 50vw;
}

.page-enter-active {
  animation-name: pushIn;
  animation-duration: 0.3s;
  animation-timing-function: ease;
}

.page-leave-active {
  animation-name: pushOut;
  animation-duration: 0.3s;
  animation-timing-function: ease-in-out;
}

@keyframes pushIn {
  0% {
    transform: translate(0px, 100vh);
  }

  100% {
    transform: translate(0px, 0px);
  }
}

@keyframes pushOut {
  0% {
    transform: translate(0px, 0px);
  }

  100% {
    transform: translate(0px, 100vh);
  }
}

a {
  color: inherit;
  text-decoration: none;
}

header {
  z-index: 99998;
  min-width: 100%;
  height: 58px;
  position: sticky;
  top: 0;
}

header>.global {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 58px;
}

header>.global>.menu {
  margin-right: 20px;
  height: 30px;
  width: 30px;
  vertical-align: middle;
  cursor: pointer;
}

header>.global>.menu>div {
  width: 28px;
  height: 2px;
  margin-top: 8px;
  vertical-align: middle;
  border-radius: 2px;
}

header>.global>.title {
  font-size: 28px;
  margin-right: 20px;
}

header>.global>.search {
  line-height: 58px;
  height: 58px;
  width: 58px;
}

</style>
