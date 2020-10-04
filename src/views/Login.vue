<template>
<div>
  <el-form ref="form" :model="form" :rules="rules" label-width="80px" class="login-box">
    <h1 class="login-title">欢迎登录</h1>
    <el-form-item label="用户名" prop="username">
      <el-input v-model="form.username"></el-input>
    </el-form-item>
    <el-form-item label="密码" prop="password">
      <el-input type="password" v-model="form.password"></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="login('form')">立即登录</el-button>
    </el-form-item>
  </el-form>
</div>
</template>

<script>
    export default {
        name: "Login",
      data()  {
          return {
            form:{
              username: '',
              password: ''
            },
            rules:{
              username:[
                { required: true,message:'请输入用户名',trigger:'blur'}
              ],
              password:[
                { required: true,message:'请输入密码',trigger:'blur'}
              ]
            }
          }
      },
      methods: {
          login: function (formName)  {
            this.$refs[formName].validate((valid) => {
              if (valid) {
                sessionStorage.setItem("isLogin","true");
                this.$store.dispatch("asyncUpdateUser",this.form);
                this.$router.push('/main');
              } else {
                this.$message.error('请输入用户名或密码');
                return false;
              }
            });
          }
      }
    }
</script>

<style scoped>
  .login-title{
    text-align: center;
    margin: 0 auto 40px auto;
    color: #303133;
  }
 .login-box {
   width: 350px;
   border: 1px solid #DCDFE6;
   margin: 180px auto;
   padding: 35px 35px 15px 35px;
   border-radius: 5px;
   -webkit-border-radius: 5px;
   -moz-border-radius: 5px;
   box-shadow: 0 0 25px #909399;
 }
</style>
