<template>

  <div>
    <div>
      查询数量：<Input v-model="countModel" style="width: 200px"/>
      <Button type="primary" @click="findList">查询</Button>
    </div>
   <Card>
    <Table class="table" :columns="pageColumns" :data="pageList" :loading="tableLoading"></Table>
  </Card>
  </div>
</template>
<script>
export default {
  data () {
    return {
      countModel:"",
      tableLoading:false,
      pageList:[],
      pageColumns:[
        {
          title:"用户id",
          key:"pin",
          minWidth:500,
          maxWidth:500,
          tooltip:true
        },
        {
          title:"关联数量",
          key:"count",
          minWidth:500,
          maxWidth:500,
          tooltip:true
        },
      ],

    }
  },
  methods: {
    findList(){
      let list = [];
      this.$axios.post("/sys/topN",{
          max:this.countModel
      }).then(result=>{
        for (let i = 0; i < result.data.data.length; i++) {
          list.push(result.data.data[i])
        }
        this.pageList = list;
      }).catch(error=>{
        console.log(error)
      });
    },
  }
}
</script>
