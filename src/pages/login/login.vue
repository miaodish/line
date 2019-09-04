<template>
  <div style="display: flex; align-items:center;height: 70vh;width: 100vw; justify-content:center;">
    <div style="flex-shrink:0;">
      <img :src="logo" mode="widthFix" alt="wrong">
      <i-input @change="changeUserName" type="text" title="账户" autofocus maxlength="12"></i-input>
      <i-input @change="changePassword" type="password" title="密码" maxlength="12"></i-input>
      <i-row>
        <i-col span="4" offset="5">
        <i-button @click="login" :inline="true" type="primary">登录</i-button>
        </i-col>
        <i-col span="4" offset="4">
        <i-button @click="routeToLogup" :inline="true" type="info">注册</i-button>
        </i-col>
      </i-row>

    </div>
    <i-toast id="toast" />
  </div>
</template>

<script>
    import logo from '../../../static/images/logo.png'
    const { $Toast } = require('../../../dist/wx/dist/base/index');
    const db = wx.cloud.database({env: 'datebase-9y50j'})

    export default {
        data() {
            return {
                logo: logo,
                userName: '',
                password: '',

            }
        },
        components:{$Toast},
        methods: {
            changeUserName(event) {
                this.userName = event.mp.detail.detail.value
            },
            changePassword(event) {
                this.password = event.mp.detail.detail.value
            },
            login() {

                $Toast({
                    content: '加载中',
                    type: 'loading'
                });
                db.collection('user').where({
                    name: this.userName,
                    password: this.password
                }).get({
                    success: function (res) {
                        // res.data 是包含以上定义的两条记录的数组
                        if(res.data.length===1)
                        {
                            $Toast({
                                content: '登陆成功',
                                type: 'sucess'
                            });
                            wx.redirectTo({url: '/pages/index/main'})
                        }
                        else{
                            $Toast({
                                content: '账户或密码错误',
                                type: 'error'
                            });
                        }
                    }
                })
            },
            routeToLogup(){
                wx.redirectTo({url: '/pages/logup/main'})
            }
        },
    }
</script>
