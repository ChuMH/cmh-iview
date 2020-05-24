<template>
  <div>
    <div>
      用户id：<Input v-model="userIdModel" style="width: 200px"/>
      <Button type="primary" @click="findList">查询</Button>
    </div>
    <Card>
      <Table stripe class="table" :columns="pageColumns" :data="pageList" :loading="tableLoading"></Table>
    </Card>
  </div>
</template>
<script>
export default {
  name: 'findPath',
  data () {
    return {
      userIdModel:"",
      tableLoading:false,
      pageList:[],
      pageColumns:[
        {
          title:"用户id",
          key:"userId",
          minWidth:500,
          maxWidth:500,
          tooltip:true
        },
        {
          title:"用户名",
          key:"name",
          minWidth:500,
          maxWidth:500,
          tooltip:true
        },
        {
          title:"与下一用户亲密度",
          key:"degree",
          minWidth:500,
          maxWidth:500,
          tooltip:true
        },
        {
          title:"年龄",
          key:"age",
          minWidth:500,
          maxWidth:500,
          tooltip:true
        },
        {
          title:"爱好",
          key:"hobby",
          minWidth:500,
          maxWidth:500,
          tooltip:true
        },
      ],

    }
  },
  methods:{
    findList(){
      let resultList = [];
      this.$axios.post("/sys/findPath",{
        userId:this.userIdModel,
      }).then(result=>{
        for (let i = 0; i < result.data.data.nodes.length; i++) {
          resultList.push(result.data.data.nodes[i])
        }
        this.pageList = resultList;
      }).catch(error=>{
        console.log(error)
      });
    },
  },
}
</script>
