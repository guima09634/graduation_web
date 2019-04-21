<template>
  <el-container>
        <el-aside width="200px">
          <el-menu default-active="1" mode="vertical"  background-color="#545c64"
      text-color="#fff"
      active-text-color="#ffd04b">
            <el-submenu index="1">
              <template slot="title">玩家管理</template>
              <el-menu-item index="1-1"><nuxt-link to="/users/userData">玩家数据查管理</nuxt-link></el-menu-item>
              <el-menu-item index="1-2">游戏登陆数据观管理</el-menu-item>
              <el-menu-item index="1-3">玩家功能3</el-menu-item>
            </el-submenu>
            <el-submenu index="2">
              <template slot="title">游戏管理</template>
              <el-menu-item index="2-1">游戏储值数据查询</el-menu-item>
              <el-menu-item index="2-2">储值订单补发</el-menu-item>
              <el-menu-item index="2-3">储值功能3</el-menu-item>
            </el-submenu>
            <el-submenu index="3">
              <template slot="title">储值管理</template>
              <el-menu-item index="3-1">储值订单查看</el-menu-item>
              <el-menu-item index="3-2">储值订单补发</el-menu-item>
              <el-menu-item index="3-3">储值功能3</el-menu-item>
            </el-submenu>
            <el-submenu index="4">
              <template slot="title">客服管理</template>
              <el-menu-item index="4-1">玩家问题</el-menu-item>
              <el-menu-item index="4-2">客服服务记录</el-menu-item>
              <el-menu-item index="4-3">玩家功能3</el-menu-item>
            </el-submenu>
          </el-menu>
        </el-aside>
        <el-main>
          <nuxt/>
        </el-main>
  </el-container>
</template>

<style>
html {
  font-family: "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*, *:before, *:after {
  box-sizing: border-box;
  margin: 0;
}

.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;
}

.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}

.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #35495e;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}
</style>

