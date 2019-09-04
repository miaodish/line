<template>
  <div style="display: flex; align-items:center;height: 100vh;width: 100vw; justify-content:center;">
    <div style="flex-shrink:0;">
      <img :src="logo" mode="widthFix" alt="wrong">
      <i-row>
        <i-col span="4" offset="5">
          <i-button @click="backToLogin" :inline="true" type="primary">返回登录</i-button>
        </i-col>
        <i-col span="4" offset="4">
          <i-button @click="logup" :inline="true" type="info">完成注册</i-button>
        </i-col>
      </i-row>

    </div>
  </div>
</template>
<script>
    import logo from '../../../static/images/logo.png'
    const db = wx.cloud.database({env: 'datebase-9y50j'})

    export default {
        data() {
            return {
                logo: logo,
            }
        },
        methods:{
            logup(){
                return 0
            },
            backToLogin(){
                wx.redirectTo({url: '/pages/login/main'})
            }
        }
    }
</script>
