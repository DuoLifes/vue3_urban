<template>
  <div>
    <el-button type="primary" @click="back()">返回首页</el-button>
    <el-button type="primary" @click="logout()">退出登录</el-button>
  </div>
</template>
<script setup lang="ts">
import { useRouter, useRoute } from 'vue-router'
//获取用户相关的小仓库
import useUserStore from '@/store/modules/user'
//获取骨架的小仓库
let userStore = useUserStore()
//获取路由器对象
let $router = useRouter()
//获取路由对向
let $route = useRoute()

//退出登录点击回调
const logout = async () => {
  //第一件事情:需要向服务器发请求[退出登录接口]******
  //第二件事情:仓库当中关于用于相关的数据清空[token|username|avatar]
  //第三件事情:跳转到登录页面
  await userStore.userLogout()
  //跳转到登录页面
  $router.push({ path: '/login', query: { redirect: $route.path } })
}
const back = () => {
  $router.push({ path: '/home' })
}
</script>
