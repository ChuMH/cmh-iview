<template>
  <div>
    <Card class="warp-card" dis-hover>
      <Form :label-width="80" :model="form">
        <FormItem class="marginBottom20" label="收件人" prop="toEmails">
          <Input class="addressWidth" placeholder="请输入对方邮箱" v-model="form.to"></Input>
        </FormItem>
        <FormItem class="marginBottom20" label="标题" prop="title">
          <Input class="addressWidth" placeholder="请输入标题" v-model="form.title"></Input>
        </FormItem>
        <FormItem label="内容" required>
          <textarea v-model="form.content"></textarea>
        </FormItem>
        <FormItem>
          <Button
            :loading="isShowSaveButtonLoading"
            @click="addOrUpdateEmail"
            type="primary"
          >发送</Button>
        </FormItem>
      </Form>
    </Card>
  </div>
</template>
<script>
  export default {
    data(){
      return{
        form:{
          title:"",
          to:"",
          content:""
        },
        isShowSaveButtonLoading:false,
      };
    },
    methods:{
      addOrUpdateEmail(){
        let params = this.form;
        this.$axios.post("/send/mail",{
          to:params.to,
          title:params.title,
          content:params.content
        }).then(result=>{
          if(result.data.code == 0){
            this.$Message.success("发送成功!");
            this.form = {};
          }else {
            this.$Message.error("发送失败!");
          }
        }).catch(error=>{

        });
      }
    },
  }
</script>
<style lang="less" scoped>
  .addressWidth {
    width: 350px;
  }
  .marginTop20 {
    margin-top: 20px;
  }
  .marginBottom20 {
    margin-bottom: 20px;
  }
</style>
