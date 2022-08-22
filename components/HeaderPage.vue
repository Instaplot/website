<template>
  <el-header>
    <el-row>
      <el-col :span="24">
        <el-breadcrumb separator="/">
          <el-breadcrumb-item>
            <router-link to="/">Home</router-link>
          </el-breadcrumb-item>
          <el-breadcrumb-item>
            <router-link to="/contact">Contact</router-link>
          </el-breadcrumb-item>
        </el-breadcrumb>
      </el-col>
    </el-row>
  </el-header>
</template>
