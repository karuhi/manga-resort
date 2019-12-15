<template>
  <header class="color_white background_maincolor">
    <div class="global">
      <div class="search">&nbsp&nbsp&nbsp&nbsp</div>
      <div class="title">
            <template>
              <v-lazy-image :src="`${logoImageUrl}`" :src-placeholder="`${loadingImageUrl}`" />
            </template>
      </div>
      <div class="menu" @click="toggleMenu=!toggleMenu">
        <!--<div class="background_white" v-for="n in 3"></div>-->
      </div>
    </div>
  </header>
</template>
<script>
import logoImage from '../assets/logo.png';
import loadingImage from '../assets/spinner.gif';

export default {
  data() {
    return {
      toggleMenu: false,
      loadingImageUrl: loadingImage,
      logoImageUrl: logoImage
    }
  }
}

</script>
<style scoped>
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
  margin-top: 10px;
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

</style>
