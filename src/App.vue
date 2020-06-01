<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">番茄鐘</router-link> |
      <router-link to="/list">清單</router-link> |
      <router-link to="/settings">音效</router-link>
    </div>
    <keep-alive>
      <router-view/>
    </keep-alive>
  </div>
</template>

<style lang="stylus">
*
  // font-family '微軟正黑體'
</style>
