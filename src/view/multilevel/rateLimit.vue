<template>
  <div>
    <Button @click="countLimit" type="primary">次数</Button>
    <Button @click="rateLimit" type="primary">速率</Button>
    <Button @click="ipLimit" type="primary">ip限流</Button>
    <Button @click="pinLimit" type="primary">pin限流</Button>
  </div>
</template>
<script>
export default {
  name: 'rateLimit',
  data(){
    return{};
  },
  methods:{
    countLimit(){
      this.$axios.post("/rate/limit/count",{}).then(result=>{
        this.$Message.info(result.data.msg)
      }).catch(error=>{
        console.log(error)
      })
    },
    rateLimit(){
      this.$axios.post("/rate/limit/count",{}).then(result=>{
        this.$Message.info(result.data.msg)
      }).catch(error=>{
        console.log(error)
      })
    },
    ipLimit(){
      this.$axios.post("/rate/limit/ip",{}).then(result=>{
        this.$Message.info(result.data.msg)
      }).catch(error=>{
        console.log(error)
      })
    },
    pinLimit(){
      this.$axios.post("/rate/limit/pin",{}).then(result=>{
        this.$Message.info(result.data.msg)
      }).catch(error=>{
        console.log(error)
      })
    },
  },
}
</script>
