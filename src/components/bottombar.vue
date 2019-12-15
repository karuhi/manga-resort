<template>
  <div class="bottom-navigation">
    <div class="row">
      <nuxt-link class="col" to="/">
      	<svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" viewBox="0 0 24 24" fill="none" stroke="#ffffff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path>
          <polyline points="9 22 9 12 15 12 15 22"></polyline>
        </svg><br><span class="tabtext">ホーム</span>
      </nuxt-link>
      <nuxt-link class="col" to="/library">
        <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" viewBox="0 0 24 24" fill="none" stroke="#ffffff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M6 2L3 6v14c0 1.1.9 2 2 2h14a2 2 0 0 0 2-2V6l-3-4H6zM3.8 6h16.4M16 10a4 4 0 1 1-8 0" />
        </svg><br><span class="tabtext">本棚</span>
      </nuxt-link>
      <nuxt-link class="col" to="/bookmark">
        <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" viewBox="0 0 24 24" fill="none" stroke="#ffffff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M20.59 13.41l-7.17 7.17a2 2 0 0 1-2.83 0L2 12V2h10l8.59 8.59a2 2 0 0 1 0 2.82z"></path>
          <line x1="7" y1="7" x2="7" y2="7"></line>
        </svg><br><span class="tabtext">しおり</span>
      </nuxt-link>
    </div>
  </div>
</template>
<style scoped>
a {
	text-decoration: none;
}
.bottom-navigation {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 99999;
  height: 58px;
}

.bottom-navigation>.row {
  display: flex;
}

.bottom-navigation>.row>.col {
  padding: 8px 0 8px 0;
  width: 100%;
  height: 100px;
  background-color: #0F4C81;
  color: white;
  font-size: 0.6em;
}
.tabtext {
	color: rgba(255,255,255,0.7);
}

</style>
