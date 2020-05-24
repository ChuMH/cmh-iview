<style lang="less">
  @import './register.less';
</style>

<template>
  <div class="register">
    <div class="register-con">
      <Card icon="log-in" title="欢迎注册" :bordered="false">
        <div class="form-con">
          <reg-form @on-success-valid="handleSubmit"></reg-form>
          <p class="register-tip">输入完整注册信息</p>
        </div>
      </Card>
    </div>
  </div>
</template>

<script>
import RegForm from '@/components/reg-form/register-form'
import { mapActions } from 'vuex'
export default {
  components: {
    RegForm
  },
  methods: {

    handleSubmit ({ email,userName, password }) {
      let params = {};
      params.email = email;
      params.userName = userName;
      params.password = password;
      this.$axios.post("/user/register",{
        email:params.email,
        userName:params.userName,
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
