<!-- eslint-disable vue/require-v-for-key -->
<template>
  <el-container>
    <el-header> Instaplot </el-header>
    <el-main>
      <div class="book-info">
        <el-alert
          v-if="state === 'bookNotFound'"
          type="error"
          effect="dark"
          title="The requested book was not found!"
        ></el-alert>
        <img src="@/static/icon.png" class="logo" />
        <h1 class="info-heading">Get information about books with ease</h1>
        <el-input
          v-model="bookInput"
          type="text"
          size="medium"
          resize="horizontal"
          class="book-input"
          @keyup.enter.native="getBookInfo"
        >
        </el-input>
        <el-button id="submit-button" type="primary" @click="getBookInfo"
          >Submit</el-button
        >
        <div v-if="state == 'info'">
          <h3 v-if="book.title">Book Title</h3>
          {{ book.title }}
          <br />
          <el-image
            v-if="book.thumbnailURL"
            :src="book.thumbnailURL"
          ></el-image>
          <h3 v-if="book.authors">Authors</h3>
          <ul>
            <li v-for="author in book.authors">{{ author }}</li>
          </ul>
          <h3 v-if="book.publisher">Publisher</h3>
          {{ book.publisher }}
          <h3 v-if="book.publishedDate">Published Date</h3>
          {{ book.publishedDate }}
          <h3 v-if="book.description">Description</h3>
          {{ book.description }}
        </div>
      </div>
    </el-main>
    <el-footer>
      <adsbygoogle />
    </el-footer>
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
        const button = document.getElementById("submit-button")
        button.setAttribute("disabled", "true");
        button.setAttribute("loading", "true");
        const book = await getBook(this.bookInput)
        if (book === 1) {
          // eslint-disable-next-line no-unused-expressions, no-sequences
          this.$alert("The requested book coundnt be found.", "Book Not Found"), {
            confirmButtonText: "OK",
            callback: action => {
              this.$message({type: "error", message: `action: ${ action }`});
            }
          }
          button.removeAttribute("loading");
          button.removeAttribute("disabled");
          return;
        }
        this.book = book;
        this.state = "info";
        button.removeAttribute("loading");
        button.removeAttribute("disabled");
      }
    }
  },
  head: {
    title: "Instaplot",
    meta: [
      {
        hid: 'description',
        name: 'description',
        content: 'Website to get information about books'
      },
      {
        hid: 'keywords',
        name: 'keywords',
        content: 'books, information, search, free, easy, website'
      },
      {
        hid: 'og:title',
        name: 'og:title',
        content: 'instaplot'
      }
    ]
  }
})
</script>

<style lang="scss" scoped>
.book-info {
  text-align: center;
}

.book-input {
  width: 20rem;
}

.info-heading {
  color: yellowgreen;
}

.logo {
  position: relative;
  width: 8rem;
  right: 1rem;
}
</style>
