<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <el-container>
    <el-header>
      <HeaderPage />
    </el-header>
    <el-main>
      <el-alert
        v-if="state === '429'"
        type="error"
        effect="dark"
        title="Rate limit exceeded! Please try again in a minute."
      ></el-alert>
      <el-form
        label-position="left"
        :model="contact"
        label-width="100px"
        size="small"
        accept-charset="UTF-8"
      >
        <el-form-item label="Name" prop="name" name="name">
          <el-input v-model="contact.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item
          label="Email"
          prop="email"
          name="email"
          :rules="rulesEmail"
        >
          <el-input v-model="contact.email" autocomplete="on"></el-input>
        </el-form-item>
        <el-form-item
          label="Message"
          prop="message"
          name="message"
          :rules="rulesMessage"
        >
          <el-input
            v-model="contact.message"
            type="textarea"
            autocomplete="off"
          ></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="submitForm">Submit</el-button>
        </el-form-item>
      </el-form>
    </el-main>
  </el-container>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      state: 'default',
      error: '',
      rulesEmail: [
        {
          required: true,
          message: 'Please input email address',
          trigger: 'blur',
        },
        {
          type: 'email',
          message: 'Please input correct email address',
          trigger: ['blur', 'change'],
        },
      ],
      rulesMessage: [
        {
          required: true,
          message: 'Please input message',
          trigger: 'blur',
        },
        {
          min: 10,
          message: 'Please input at least 5 characters',
          trigger: 'blur',
        },
      ],
      contact: {
        name: '',
        email: '',
        message: '',
      },
      submitForm: async () => {
        try {
          // eslint-disable-next-line no-unused-vars
          const response = await axios.post(
            'https://getform.io/f/7e13e905-e37a-4653-bc70-e70c5f73fb0f',
            this.contact
          )
          alert('Submited')
        } catch (error) {
          const e = error.toString()
          if (e.includes('429')) {
            this.state = '429'
          } else {
            alert('An error occurred! ' + error)
          }
        }
      },
    }
  },
}
</script>

<style></style>
