<template>
  <header class="color_white background_black">
    <div class="global">
      <div class="search">&nbsp&nbsp&nbsp&nbsp</div>
      <div class="title">MANGA RESORT</div>
      <div class="menu" @click="toggleMenu=!toggleMenu">
        <div class="background_white" v-for="n in 3"></div>
      </div>
    </div>
    <div class="category_list">
      <div class="category_m background_skyblue" v-for="(element, index) in tags">
        {{element}}
      </div>
    </div>
    <div class="toggleMenu background_black" v-show="toggleMenu">
      <div class="Search">
        <input type="text" name="SearchBar" class="SearchBar" placeholder="記事を検索...">
        <button class="SearchButton background_skyblue color_white">検索</button>
      </div>
      <div class="text_left">タグ</div>
      <div class="category_list">
        <div class="category_l background_skyblue" v-for="(element, index) in tags">
          {{element}}
        </div>
      </div>
      <div class="text_left">日付</div>
      <div class="category_list">
        <div class="category_l background_skyblue" v-for="(element, index) in date">
          {{element}}
        </div>
      </div>
      <div class="text_left">おすすめの投稿</div>
      <div class="featured_list">
        <div v-for="(element, index) in json" v-if="element.featured" class="list">
          <img :src="element.image">
          <div class="title">{{element.title}}</div>
        </div>
      </div>
    </div>
  </header>
</template>
<script>
export default {
  props: ['json'],
  data() {
    return {
      tags: ['講談社', '新潟書店', '京田辺書店', 'Patreon'],
      date: ['2019.5', '2019.4', '2019.3', '2019.2', '2019.1', '2018.12', '2018.11', '2018.10', '2018.9', ],
      toggleMenu: false
    }
  }
}

</script>
<style scoped>
header {
  z-index: 99998;
  min-width: 100%;
  height: 108px;
  position: sticky;
  top: 0;
}

header>.global {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 68px;
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
}

header>.global>.search {
  margin-right: 20px;
}

header>.category_list {
  height: 40px;
  overflow-x: auto;
  white-space: nowrap;
  -webkit-overflow-scrolling: touch;
}

header>.category_list>div:nth-child(1) {
  display: inline-block;
  margin: 5px 10px 5px 10px;
  height: 20px;
  width: 80px;
}

header>.category_list>div {
  display: inline-block;
  margin: 5px 10px 5px 0px;
  height: 20px;
  width: 80px;
}
.toggleMenu {
  z-index: 99999;
  position: fixed;
  top: 68px;
  bottom: 0;
  left: 0;
  right: 0;
  width: 100vw;
  height: 100vh;
}

.toggleMenu>.Search {
  height: 60px;
}

.toggleMenu>.Search>.SearchBar {
  margin-top: 10px;
  height: 40px;
  width: 100%;
  max-width: calc(100% - 80px);
  border-radius: 5px 0 0 5px;
  border-style: none;
  padding-left: 10px;
}

.toggleMenu>.Search>.SearchButton {
  margin-left: -5px;
  height: 40px;
  width: 40px;
  border-radius: 0 5px 5px 0;
  border-style: none;
}

.toggleMenu>.category_list {
  margin-left: 20px;
  height: 50px;
  overflow-x: auto;
  white-space: nowrap;
  -webkit-overflow-scrolling: touch;
}

.toggleMenu>.category_list>div:nth-child(1) {
  display: inline-block;
  margin: 10px;
  height: 30px;
  width: 80px;
}

.toggleMenu>.category_list>div {
  display: inline-block;
  margin: 10px 10px 10px 0px;
  height: 30px;
  width: 80px;
}

header>.category_list::-webkit-scrollbar,
.toggleMenu>.category_list::-webkit-scrollbar,
.toggleMenu>.featured_list::-webkit-scrollbar {
  height: 5px;
}

header>.category_list::-webkit-scrollbar-track,
.toggleMenu>.category_list::-webkit-scrollbar-track,
.toggleMenu>.featured_list::-webkit-scrollbar-track {
  background: #1E1B18;
}

header>.category_list::-webkit-scrollbar-thumb,
.toggleMenu>.category_list::-webkit-scrollbar-thumb,
.toggleMenu>.featured_list::-webkit-scrollbar-thumb {
  background: #3E92CC;
  border-radius: 5px;
}

.toggleMenu>.featured_list {
  margin-left: 20px;
  height: 180px;
  overflow-x: auto;
  white-space: nowrap;
  -webkit-overflow-scrolling: touch;
}

.toggleMenu>.featured_list>.list {
  margin: 10px 20px 10px 0;
  display: inline-block;
    position: relative;
}
.toggleMenu>.featured_list>.list>img {
  border-radius: 5px;
  height: 120px;
  width: 160px;
}
.toggleMenu>.featured_list>.list>.title {
  position: absolute;
  word-wrap: break-word;
  white-space: normal;
  width: 140px;
  height: 30px;
  margin-left:10px;
  font-size: 12px;
}
.text_left {
  margin-left: 20px;
  margin-top: 20px;
  text-align: left;
}

</style>
