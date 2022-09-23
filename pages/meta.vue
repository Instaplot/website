<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <el-container>
    <el-header>
      <HeaderPage />
    </el-header>
    <el-main>
      <div id="meta" class="center">
        Author: Vaibhav Dhiman <br />
        <a href="https://github.com/Instaplot"> Source </a> <br />
        The books are fetched using Google Books API. <br />
        Element UI Library is used for UI. <br />
        The website was made using Nuxt.js. <br />
        The searched are not logged by us, Instaplot.
      </div>
      <div v-if="allowAds">
        <script
          async="async"
          data-cfasync="false"
          src="//pl17695264.profitablegatetocontent.com/91460dac0ef7119861e1a676c24940a1/invoke.js"
        ></script>
        <div id="container-91460dac0ef7119861e1a676c24940a1"></div>
        <script
          type="text/javascript"
          src="//pl17695220.profitablegatetocontent.com/bb/5b/88/bb5b889b06ba211190c1906d5ae0f667.js"
        ></script>
      </div>
    </el-main>
  </el-container>
</template>

<script lang="js">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
  data() {
    return {
      state: "default",
      allowAds: false,
    }
  },
  head: {
    title: "Meta - Instaplot",
    meta: [
      {
        hid: 'description',
        name: 'description',
        content: 'Meta information about instaplot'
      },
      {
        hid: 'keywords',
        name: 'keywords',
        content: 'meta, books, information, search, free, easy, website'
      },
      {
        hid: 'og:title',
        name: 'og:title',
        content: 'meta'
      }
    ],
  }
})
</script>

<style lang="scss" scoped>
.center {
  padding: 70px 0;
  text-align: center;
}

img {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50px;
  height: 50px;
}
</style>
