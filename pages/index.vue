<!-- eslint-disable vue/require-v-for-key -->
<template>
  <el-container>
    <el-main>
      <div align="center">
        <el-input
          v-model="bookInput"
          type="text"
          size="medium"
          resize="horizontal"
          class="book-input"
        >
        </el-input>
        <el-button type="primary" @click="getBookInfo">Submit</el-button>
        <div v-if="state == 'info'">
          <h3>Book Title</h3>
          {{ book.title }}
          <br />
          <el-image :src="book.thumbnailURL"></el-image>
          <h3>Authors</h3>
          <ul>
            <li v-for="author in book.authors">{{ author }}</li>
          </ul>
          <h3>Publisher</h3>
          {{ book.publisher }}
          <h3>Published Date</h3>
          {{ book.publishedDate }}
          <h3>Description</h3>
          {{ book.description }}
        </div>
      </div>
    </el-main>
  </el-container>
</template>

<script lang="js">
import Vue from 'vue'
import { getBook } from 'instaplot'

export default Vue.extend({
  name: 'IndexPage',
  data() {
    return {
      state: "default",
      bookInput: "",
      book: {},
      getBookInfo: async () => {
        this.disabled = true;
        this.book = await getBook(this.bookInput)
        this.disabled = false;
        this.state = "info";
      }
    }
  },
})
</script>
