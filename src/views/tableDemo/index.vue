<template>
  <div class="app-container">
        <span>测试班级_任务1_组2组 基本统计汇总</span>
      <el-table
        :data="tableData"
        highlight-current-row
        border
        style="width: 100%">
        <el-table-column
          type="index"
          width="100px"
          align="center"
        >
        </el-table-column>
        <el-table-column
          prop="name"
          align="center"
          label="统计项目 / 成员">
        </el-table-column>
        <el-table-column
          prop="tallNum"
          align="center"
          label="讨论数">
        </el-table-column>
        <el-table-column
          prop="tallDate"
          align="center"
          label="参与讨论时长(天)">
        </el-table-column>
        <el-table-column
          prop="speakNum"
          align="center"
          label="互动情况@数">
        </el-table-column>
        <el-table-column
          prop="speakCondition"
          align="center"
          label="互动情况被@数">
        </el-table-column>
      </el-table>

      <!--分页-->
      <div class="clear_right">
        <el-pagination
          @size-change="handleSizeChangeGroup"
          @current-change="handleCurrentChangeGroup"
          :current-page="currentPage"
          :page-sizes="[5,10,20]"
          :page-size="pageSize"
          layout="total, sizes, prev, pager, next, jumper"
          :total="totalCount">
        </el-pagination>
      </div>
    </div>
</template>

<script>
  export default {
    components:{
    },
    name: 'tableDemo',
    data() {
      return {

        totalCount:50,
        currentPage:1,
        pageSize:10,
        condition:"",
        tableData:[
          {
            name:"张三",
            tallNum:"103",
            tallDate:"34",
            speakNum:"26",
            speakCondition:"344"
          },{
            name:"李四",
            tallNum:"23",
            tallDate:"3",
            speakNum:"6",
            speakCondition:"562"
          },{
            name:"王五",
            tallNum:"103",
            tallDate:"34",
            speakNum:"26",
            speakCondition:"344"
          },{
            name:"赵柳",
            tallNum:"13",
            tallDate:"66",
            speakNum:"42",
            speakCondition:"683"
          },{
            name:"水电费",
            tallNum:"13",
            tallDate:"74",
            speakNum:"54",
            speakCondition:"56"
          },{
            name:"闪电发",
            tallNum:"77",
            tallDate:"34",
            speakNum:"26",
            speakCondition:"34344"
          },{
            name:"闪电发",
            tallNum:"77",
            tallDate:"34",
            speakNum:"26",
            speakCondition:"34344"
          },{
            name:"闪电发",
            tallNum:"77",
            tallDate:"34",
            speakNum:"26",
            speakCondition:"34344"
          },{
            name:"闪电发",
            tallNum:"77",
            tallDate:"34",
            speakNum:"26",
            speakCondition:"34344"
          },{
            name:"闪电发",
            tallNum:"77",
            tallDate:"34",
            speakNum:"26",
            speakCondition:"34344"
          }
        ]
      }
    },
    created(){
    },
    watch:{
      "$route":function(to,from){
        console.log(to)
      }
    },
    mounted(){
    },
    methods:{
      handleSizeChangeGroup(val){
        this.pageSize=val;
        this.getDataFromTempGroup(this.currentPage,this.pageSize,this);
      },
      handleCurrentChangeGroup(val){
        this.currentPage=val;
        this.getDataFromTempGroup(this.currentPage,this.pageSize,this);
      },
      getDataFromTempGroup(page,size,objName){
        //初始化数据
          objName.tableData.filter(item=>item.groupName.indexOf(objName.condition) != -1 );
        objName.totalCount = objName.tableData.length;
        var start = ( objName.currentPage -1 )* objName.pageSize;
        objName.tableData = objName.tableData.slice(start,start + objName.pageSize);
      },
    }
  }
</script>

<style scoped>
  .app-container{
    padding-top: 10px;
  }
.app-container span{
  display: block;
  text-align: center;
  padding:5px auto;

  font-size: 25px;
  margin: 0px auto 20px auto;
}
</style>
