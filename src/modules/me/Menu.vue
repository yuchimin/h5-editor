<template>
  <el-menu default-active="projects-0" @select="onSelect" class="me-menu">
    <el-submenu index="projects">
      <template slot="title">
        <i class="el-icon-location"></i>
        <span slot="title">我的项目</span>
      </template>
      <el-menu-item index="projects-0">我发起的项目</el-menu-item>
      <el-menu-item index="projects-1">我参与的项目</el-menu-item>
    </el-submenu>

    <el-submenu index="collects">
      <template slot="title">
        <i class="el-icon-menu"></i>
        <span slot="title">我的收藏</span>
      </template>
      <el-menu-item index="projects-2">项目</el-menu-item>
      <el-menu-item index="templs-1">模版</el-menu-item>
      <el-menu-item index="comps-1">组件</el-menu-item>
    </el-submenu>

    <el-menu-item index="templs-0">
      <i class="el-icon-document"></i>
      <span slot="title">我的模版</span>
    </el-menu-item>
    <el-menu-item index="comps-0">
      <i class="el-icon-setting"></i>
      <span slot="title">我的组件</span>
    </el-menu-item>
    <el-menu-item index="mods-0">
      <i class="el-icon-setting"></i>
      <span slot="title">我的模块</span>
    </el-menu-item>
  </el-menu>
</template>

<script>
  export default {
    name: 'Menu',
    data () {
      return {}
    },
    methods: {
      onSelect (index) {
        const type = index.split('-')[0]
        const key = parseInt(index.split('-')[1])
        this.$emit('select', { type, key })
      }
    }
  }
</script>

<style>
.me-menu {
  min-height: calc(100vh - 240px);
}
.el-menu-vertical-demo:not(.el-menu--collapse) {
  width: 200px;
  min-height: 400px;
}
</style>

