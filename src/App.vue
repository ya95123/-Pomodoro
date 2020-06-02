<template>
  <div id="app">
    <div id="nav">
      <!-- 跳出側邊攔按鈕 -->
      <b-img id="edit" src="../public/img/user/pencil.png" alt="編輯" v-b-toggle.sidebar-right></b-img>
      <!-- 側邊攔 -->
      <b-sidebar id="sidebar-right" class="position-relative" bg-variant="transparent" right no-header>
        <!-- 關視窗模板 -->
        <!-- <template v-slot:default="{ hide }"> -->
          <!-- 關視窗紐 -->
          <!-- <div id="xIcon" class="text-white text-center" @click="hide">×</div> -->
          <div id="sidebar-container" class="px-3 py-2 position-absolute">
          <!-- 首頁 -->
            <router-link to="/" class="mt-2"><b-img src="../public/img/user/tomato.png" alt="首頁" fluid></b-img></router-link>
          <!-- 清單 -->
            <router-link to="/list" class="mt-5"><b-img src="../public/img/user/checklist.png" alt="清單" fluid></b-img></router-link>
          <!-- 鈴聲 -->
            <router-link to="/settings" class="mt-5"><b-img src="../public/img/user/bell.png" alt="音效" fluid></b-img></router-link>
          </div>
        <!-- </template> -->
      </b-sidebar>
    </div>

    <!-- storage、router -->
    <keep-alive>
      <router-view/>
    </keep-alive>
  </div>
</template>

<script>
export default {

}
</script>

      <!-- <div id="editItem">
        <router-link to="/"><img src="../public/img/user/browser.png" alt="番茄鐘"></router-link> |
        <router-link to="/list"><img src="../public/img/user/checklist.png" alt="清單"></router-link> |
        <router-link to="/settings"><img src="../public/img/user/bell.png" alt="音效"></router-link>
      </div> -->
