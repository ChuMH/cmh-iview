<style lang="less">
  @import './login.less';
</style>

<template>
  <div class="login">
    <div class="login-con">
      <Card icon="log-in" title="欢迎登录" :bordered="false">
        <div class="form-con">
          <login-form @on-success-valid="handleSubmit"></login-form>
          <p class="login-tip">输入任意用户名和密码即可</p>
        </div>
      </Card>
    </div>
  </div>
</template>

<script>
import LoginForm from '_c/login-form'
import { mapActions } from 'vuex'
export default {
  components: {
    LoginForm
  },
  methods: {
    ...mapActions([
      'handleLogin',
      'getUserInfo'
    ]),
    handleSubmit ({ userName, password }) {
      let params = {};
      params.email = userName;
      params.password = password;
      this.$axios.post("/user/login",{
        email:params.email,
        password:params.password
      }).then(result=>{
        if (result.data && result.data.success) {
          this.$router.push({
            name: this.$config.homeName
          })
        }else {
          this.$Message.error(result.data.msg)
        }
      }).catch(
        error=>{
          console.log(error)
        }
      );
      // this.handleLogin({ userName, password }).then(res => {

      //   this.getUserInfo().then(res => {

        // })
      // })
    }
  }
}
</script>

<style>

</style>
