<template>
  <div class="container">
    <header class="color_white background_maincolor">
      <div class="global">
        <router-link class="search" to="/">X</router-link>
        <div class="title">MANGA RESORT</div>
        <div>&nbsp&nbsp&nbsp&nbsp</div>
      </div>
    </header>
    <div class="description">
      <div class="seriesImage">
        <div class="seriesImage-content" :style="{ backgroundImage: `url(${seriesData.seriesImage})`}">
          <template>
            <v-lazy-image :src="`${seriesData.seriesImage}`" :src-placeholder="`${loadingImageUrl}`" />
          </template>
        </div>
      </div>
      <div class="overlay-volumes">
        全{{seriesData.volumes}}巻
      </div>
      <div class="content">
        <div class="title">
          {{seriesData.title}}
        </div>
        <div class="authorAndPubs">著 {{seriesData.author}}, 出版社 {{seriesData.publisher}}</div>
        {{seriesData.description}}
      </div>
    </div>
    <div class="manga-container">
      <router-link class="manga-card" v-for="(element, index) in seriesData.books" v-bind:to="`/bookViewer/${ element.id }`">
        <div class="meta">
          <div class="photo">
            <template>
              <v-lazy-image :src="`${element.image}`" :src-placeholder="`${loadingImageUrl}`" />
            </template>
          </div>
        </div>
        <div class="description">
          <h1>{{ element.title}}</h1>
          <h2>全{{seriesData.books.length}}巻中 {{index+1}}巻</h2>
        </div>
      </router-link>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
import loadingImage from '../../assets/spinner.gif';

export default {
  components: {},
  data: function() {
    return {
      loadingImageUrl: loadingImage
    }
  },
  mounted: function() {},
  methods: {},
  async asyncData({ params }) {
    const myHttpClient = axios.create({
      baseURL: "https://wfc2-image-api-259809.appspot.com/api/"
    })
    const data = await Promise.all([
      myHttpClient.get('series/' + params.id)
    ])
    console.log(data);
    return { seriesData: data[0].data };
  }
}

</script>
<style scoped>
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

.page-enter {}

.page-leave-active {}
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

.description>.content {
  margin: 8px;
}

.description>.content>.authorAndPubs {
  font-size: 0.8rem;
  color: rgba(0, 0, 0, 0.6);

}

.overlay-volumes {
  width: 64px;
  height: 64px;
  background-color: red;
  position: absolute;
  top: calc(30vh - 16px);
  right: 8px;
  border-radius: 50%;
  line-height: 64px;
  color: white;
}

* {
  box-sizing: border-box;
}

body {
  background: #f1f1f1;
  margin: 2rem;
}

a {
  color: inherit;
  text-decoration: none;
}

.manga-container {
  margin-top: 8px;
  margin-bottom: 8px;
  margin-left: 16px;
  margin-right: 16px;
}

.manga-card {
  display: flex;
  flex-direction: column;
  margin: 1rem auto;
  box-shadow: 0 3px 7px -1px rgba(0, 0, 0, 0.1);
  margin-bottom: 1.6%;
  background: #fff;
  line-height: 1.4;
  border-radius: 5px;
  overflow: hidden;
  z-index: 0;
}

.manga-card a {
  color: inherit;
}

.manga-card a:hover {
  color: #0F4C81;
}

.manga-card:hover .photo {
  transform: scale(1.3) rotate(3deg);
}

.manga-card .meta {
  position: relative;
  z-index: 0;
  height: 200px;
}

.manga-card .photo,
.manga-card .photo img {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-size: cover;
  background-position: center;
  transition: transform 0.2s;
}

.manga-card .photo img {

  width: 100%;
  height: 100%;
  object-fit: contain;
}

.manga-card .description {
  padding: 1rem;
  background: #fff;
  position: relative;
  z-index: 1;
}


.manga-card .description h1 {
  line-height: 1;
  margin: 0;
  font-size: 1.2rem;
}

.manga-card .description h2 {
  font-size: 1rem;
  font-weight: 300;
  text-transform: uppercase;
  color: #a2a2a2;
  margin-top: 5px;
}


.manga-card p {
  position: relative;
  margin: 1rem 0 0;
}

.manga-card p:first-of-type {
  margin-top: 1.25rem;
}

.manga-card p:first-of-type:before {
  content: "";
  position: absolute;
  height: 5px;
  background: #0F4C81;
  width: 35px;
  top: -0.75rem;
  border-radius: 3px;
}

.manga-card:hover .details {
  left: 0%;
}

@media (min-width: 0px) {
  .manga-card {
    flex-direction: row;
    max-width: 700px;
  }

  .manga-card .meta {
    flex-basis: 40%;
    height: auto;
  }

  .manga-card .description {
    flex-basis: 60%;
  }

  .manga-card .description:before {
    transform: skewX(-3deg);
    content: "";
    background: #fff;
    width: 30px;
    position: absolute;
    left: -10px;
    top: 0;
    bottom: 0;
    z-index: -1;
  }

  .manga-card.alt {
    flex-direction: row-reverse;
  }

  .manga-card.alt .description:before {
    left: inherit;
    right: -10px;
    transform: skew(3deg);
  }

  .manga-card.alt .details {
    padding-left: 25px;
  }
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

.seriesImage {
  width: 100%;
  height: 30vh;
}

.seriesImage-content {
  height: 100%;
  background-size: cover;
  position: relative;
  z-index: 0;
  overflow: hidden;
}

.seriesImage-content:before {
  content: '';
  background: inherit;
  filter: blur(5px);
  position: absolute;
  top: -5px;
  left: -5px;
  right: -5px;
  bottom: -5px;
  z-index: -1;
}

.seriesImage-content>img {
  width: 100%;
  height: 30vh;
  object-fit: contain;
}

</style>
