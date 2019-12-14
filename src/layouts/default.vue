<template>
  <div>
    <nuxt />
  </div>
</template>
<style>
html {
  /* 日本語指定 */
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Hiragino Sans", "Hiragino Kaku Gothic ProN", Meiryo, sans-serif;
  /* ボールド指定 */
  font-weight: 600;
  font-size: 18px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
  margin: 0 auto;
  min-height: 100vh;
  justify-content: center;
  text-align: center;
}
*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}


.color_white {
  color: #FFFAFF;
}

.color_black {
  color: #1E1B18;
}

.color_pink {
  color: #D8315B;
}

.color_blue {
  color: #0A2463;
}

.color_skyblue {
  color: #3E92CC;
}

.background_white {
  background-color: #FFFAFF;
}

.background_black {
  background-color: #1E1B18;
}

.background_pink {
  background-color: #D8315B;
}

.background_blue {
  background-color: #0A2463;
}

.background_darkblue {
  background-color: #222E50;
}

.background_skyblue {
  background-color: #3E92CC;
}

.category_m {
  height: 20px;
  width: 80px;
  border-radius: 5px;
  font-size: 14px;
  font-weight: bold;
}

.category_l {
  height: 30px;
  width: 80px;
  border-radius: 5px;
  font-size: 14px;
  font-weight: bold;
  box-shadow: 3px 3px 3px rgba(30, 27, 24, 0.7);
  line-height: 2;
}

.category_l_read {
  height: 30px;
  width: 100px;
  border-radius: 5px;
  font-size: 14px;
  font-weight: bold;
  box-shadow: 3px 3px 3px rgba(30, 27, 24, 0.7);
  line-height: 2;
}

</style>
