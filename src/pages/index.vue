<template>
  <div class="container">
    <navmenu />
    <!--<div class="slider" ref="slider" v-for="(element, index) in ArticleData[0].data.data">
      <div class="slider-content" :style="{ backgroundImage: `url(${element.seriesImage})`}">
        <img :src="element.seriesImage" />
      </div>
    </div>-->
    <div class="manga-container">
      <router-link class="manga-card" v-for="(element, index) in ArticleData[0].data.data" v-bind:to="`/series/${ element.seriesId }`">
        <div class="meta">
          <div class="photo">
            <template>
              <v-lazy-image :src="`${element.seriesImage}`" :src-placeholder="`${loadingImageUrl}`" />
            </template>
          </div>
        </div>
        <div class="description">
          <h1>{{ element.title}}</h1>
          <h2>全{{element.volumes}}巻</h2>
          <p> {{element.description}}</p>
        </div>
      </router-link>
    </div>
    <bottombar />
  </div>
</template>
<script>
import navmenu from '../components/navmenu.vue'
import bottombar from '../components/bottombar.vue'
import axios from 'axios'
import loadingImage from '../assets/spinner.gif';

export default {
  components: {
    navmenu,
    bottombar
  },
  data: function() {
    return {
      nowSlide: 0,
      SlideInterval: 5000,
      intervalId: undefined,
      loadingImageUrl: loadingImage
    }
  },
  mounted: function() {
    //this.Slider();
  },
  methods: {
    Slider() {
      var SlideList = this.$refs.slider;
      SlideList[0].style.display = 'block';
      this.intervalId = setInterval(this.SlidePusher, this.SlideInterval)
    },
    SlidePusher() {
      var SlideList = this.$refs.slider;
      if (this.nowSlide < SlideList.length - 1) {
        this.nowSlide = this.nowSlide + 1;
      } else {
        this.nowSlide = 0;
      }
    }
  },
  async asyncData({ env }) {
    const myHttpClient = axios.create({
      baseURL: "https://wfc2-image-api-259809.appspot.com/api/"
    })
    const data = await Promise.all([
      myHttpClient.get('series')
    ])
    console.log(data);
    return { ArticleData: data };
  },
  watch: {
    nowSlide: function(nowval, oldval) {
      var SlideList = this.$refs.slider;
      //console.log(nowval, oldval);
      SlideList[nowval].style.display = 'block';
      SlideList[oldval].style.display = 'none';
    }
  },
  beforeDestroy() {
    console.log('clearInterval');
    clearInterval(this.intervalId);
  }
}

</script>
<style scoped>
.contaner {}

.content {
  padding: 16px;
}

.series {
  background-color: #aaaaaa;
  filter: drop-shadow(10px 10px 10px rgba(0, 0, 0, 0.6));
}

.slider {
  width: 100%;
  height: 40vh;
  display: none;
}

.slider-content {
  height: 100%;
  background-size: cover;
  position: relative;
  z-index: 0;
  overflow: hidden;
}

.slider-content:before {
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

.slider-content>img {
  width: 100%;
  height: 40vh;
  object-fit: contain;
}
a {
  color: inherit;
  text-decoration: none;
}
* {
  box-sizing: border-box;
}

body {
  background: #f1f1f1;
  margin: 2rem;
}

.manga-container {
  margin-top: 8px;
  margin-bottom: 8px;
  margin-left: 16px;
  margin-right: 16px;
  padding-bottom: 58px;
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

.manga-card .photo {
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
  font-size: 1.7rem;
}

.manga-card .description h2 {
  font-size: 1rem;
  font-weight: 300;
  text-transform: uppercase;
  color: #a2a2a2;
  margin-top: 5px;
}

.manga-card .description p {
  width: 100%;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
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

@media (min-width: 640px) {
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

</style>
