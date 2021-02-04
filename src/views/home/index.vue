<template>
  <div class="app-container">
          <div class="head">
            <div>
              <div class="info">
                <span>100</span>
                <span>个人信息</span>
              </div>
              <div class="infoEnglish">Personal information</div>
              <div class="moreInfor" @click="lookMyInfor">mor infor</div>
            </div>
            <div>
              <div class="info">
                <span>100</span>
                <span>讨论组</span>
              </div>
              <div class="infoEnglish">discussion group</div>
              <div class="moreInfor"  @click="lookDiscussGroup">mor infor</div>
            </div>
            <div>
              <div class="info">
                <span>100</span>
                <span>任务</span>
              </div>
              <div class="infoEnglish">task</div>
              <div class="moreInfor" @click="lookTask">mor infor</div>
            </div>
            <div>
              <div class="info">
                <span>100</span>
                <span>当前组和人数</span>
              </div>
              <div class="infoEnglish">Group and number</div>
              <div class="moreInfor" @click="lookGroupAndPerson">mor infor</div>
            </div>
          </div>
    <div class="content">
     <!--<big-content></big-content>-->
     <statistic-detail></statistic-detail>
    </div>
    <!--个人信息弹框-->
    <el-dialog
      title="个人信息"
      :visible.sync="myInforFlag"
      width="400px">
      <el-form v-model="myInfor" label-width="95px">
        <el-form-item label="用户名：">
          <el-input v-model="myInfor.userName" style="width: 250px" disabled></el-input>
        </el-form-item>
        <el-form-item label="用户ID：">
          <el-input v-model="myInfor.userID" style="width: 250px" disabled></el-input>
        </el-form-item>
        <el-form-item label="邮箱：">
          <el-input v-model="myInfor.userEmail" style="width: 250px" disabled></el-input>
        </el-form-item>
        <el-form-item label="角色：">
          <el-input v-model="myInfor.userRole" style="width: 250px" disabled></el-input>
        </el-form-item>
        <el-form-item label="调试状态：">
          <el-input v-model="myInfor.adjustStatus" style="width: 250px" disabled></el-input>
        </el-form-item>
      </el-form>
      <!--<span slot="footer" class="dialog-footer">
  <el-button @click="allocDialogVisible = false" size="small">取 消</el-button>
  <el-button type="primary" @click="handleAllocDialogConfirm()" size="small">确 定</el-button>
  </span>-->
    </el-dialog>
    <!--讨论组-->
    <el-dialog
      title="讨论组"
      :visible.sync="discussGroup.discussGroupFlag"
      width="900px">
      <div style="margin-bottom: 10px">
        <span>讨论组名称:</span>
        <el-input v-model="discussGroup.condition" clearable style="width: 250px"></el-input>
        <el-button type="primary" size="medium" @click="searchGroupName">搜索</el-button>
      </div>
      <el-table
        :data="discussGroup.tableData"
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
          prop="groupName"
          align="center"
          label="讨论组名称">
        </el-table-column>
        <el-table-column
          label="操作"
          align="center"
          width="200px">
          <template slot-scope="scope">
            <el-button type="primary" size="mini">查看成员</el-button>
          </template>
        </el-table-column>
      </el-table>

      <!--分页-->
      <div class="clear_right">
        <el-pagination
          @size-change="handleSizeChangeGroup"
          @current-change="handleCurrentChangeGroup"
          :current-page="discussGroup.currentPage"
          :page-sizes="[5,10,20]"
          :page-size="discussGroup.pageSize"
          layout="total, sizes, prev, pager, next, jumper"
          :total="discussGroup.totalCount">
        </el-pagination>
      </div>

    </el-dialog>
      <!--任务组-->
    <el-dialog
      title="任务组"
      :visible.sync="task.taskFlag"
      width="900px">
      <div style="margin-bottom: 10px">
        <span>讨论组名称:</span>
        <el-input v-model="task.condition" clearable style="width: 250px"></el-input>
        <el-button type="primary" size="medium" @click="searchTaskName">搜索</el-button>
      </div>
      <el-table
        :data="task.tableData"
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
          prop="taskName"
          align="center"
          label="任务组名称">
        </el-table-column>
        <el-table-column
          label="操作"
          align="center"
          width="200px">
          <template slot-scope="scope">
            <el-button type="primary" size="mini">查看成员</el-button>
          </template>
        </el-table-column>
      </el-table>

      <!--分页-->
      <div class="clear_right">
        <el-pagination
          @size-change="handleSizeChangeTask"
          @current-change="handleCurrentChangeTask"
          :current-page="task.currentPage"
          :page-sizes="[5,10,20]"
          :page-size="task.pageSize"
          layout="total, sizes, prev, pager, next, jumper"
          :total="task.totalCount">
        </el-pagination>
      </div>

    </el-dialog>

    <el-dialog
      title="任务小组第三讨论组"
      :visible.sync="groupAndPerson.groupAndPersonFlag"
      width="900px">
          <!--当前组和人数-->
    <div style="margin-bottom: 10px">
      <el-button type="primary" size="medium">点击下载</el-button>
    </div>
    <el-table
      :data="groupAndPerson.tableData"
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
        label="头像"
        align="center"
        width="70px">
        <template slot-scope="scope">
          <img src="../../../static/touxiang/test.jpg" width="35" height="35"/>
        </template>
      </el-table-column>
      <el-table-column
        prop="userName"
        align="center"
        label="人名">
      </el-table-column>
    </el-table>

    <!--分页-->
    <div class="clear_right">
      <el-pagination
        @size-change="handleSizeChangeGroupAndPerson"
        @current-change="handleCurrentChangeGroupAndPerson"
        :current-page="groupAndPerson.currentPage"
        :page-sizes="[5,10,20]"
        :page-size="groupAndPerson.pageSize"
        layout="total, sizes, prev, pager, next, jumper"
        :total="groupAndPerson.totalCount">
      </el-pagination>
        </div>
    </el-dialog>
    </div>
</template>

<script>
  import bigContent from '../../../../mall-admin-web-master/src/components/bigScreem/bigContent';
  import StatisticDetail from '../../../../mall-admin-web-master/src/components/statisticdetail/StatisticDetail';

  export default {
    components:{
      bigContent,
      StatisticDetail
    },
    name: 'home',
    data() {
      return {
        myInforFlag:false,

        taskFlag:false,
        myInfor:{
          userName:"张三",
          userID:"ZhangSan",
          userEmail:"895888950@qq.com",
          userRole:"超级管理员",
          adjustStatus:"true",
        },
        discussGroup:{
          discussGroupFlag:false,
          totalCount:50,
          currentPage:1,
          pageSize:10,
          condition:"",
          tableData:[],
          tableDataTemp:[
            {
              groupName:"组名一"
            },{
              groupName:"组名二"
            },{
              groupName:"组名三"
            },{
              groupName:"组名三"
            },{
              groupName:"组名三"
            },{
              groupName:"组名三"
            },{
              groupName:"组名三"
            },{
              groupName:"组名三3"
            },{
              groupName:"组名三2"
            },{
              groupName:"组名三1"
            },{
              groupName:"组名三1"
            },{
              groupName:"组名三4"
            },{
              groupName:"组名三5"
            },{
              groupName:"组名三"
            }
          ]
        },task:{
          taskFlag:false,
          totalCount:50,
          currentPage:1,
          pageSize:10,
          condition:"",
          tableData:[],
          tableDataTemp:[
            {
              taskName:"任务一"
            },{
              taskName:"任务一"
            },{
              taskName:"任务一"
            },{
              taskName:"任务一"
            },{
              taskName:"任务一"
            },{
              taskName:"任务一"
            },{
              taskName:"任务一"
            },{
              taskName:"任务一"
            },{
              taskName:"任务一"
            },{
              taskName:"任务一"
            }
          ]
        },
        groupAndPerson:{
          groupAndPersonFlag:false,
          totalCount:10,
          currentPage:1,
          pageSize:5,
          condition:"",
          tableData:[],
          tableDataTemp:[
            {
              userName:"张三"
            },{
              userName:"李四"
            },{
              userName:"王五"
            }, {
              userName:"赵柳"
            }, {
              userName:"任务一"
            }, {
              userName:"任务一"
            }, {
              userName:"任务一"
            }, {
              userName:"任务一"
            }
          ]
        },
      }
    },
    created(){
      // console.log(this.$route)
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
        this.discussGroup.pageSize=val;
        this.getDataFromTempGroup(this.discussGroup.currentPage,this.discussGroup.pageSize,this.discussGroup);
      },
      handleCurrentChangeGroup(val){
        this.discussGroup.currentPage=val;
        this.getDataFromTempGroup(this.discussGroup.currentPage,this.discussGroup.pageSize,this.discussGroup);
      },
      handleCurrentChangeGroupAndPerson(val){
        this.groupAndPerson.currentPage=val;
        this.getDataFromTempGroupAndPerson(this.groupAndPerson.currentPage,this.groupAndPerson.pageSize,this.groupAndPerson);
      },
      handleSizeChangeTask(val){
        this.task.pageSize=val;
        this.getDataFromTempTask(this.task.currentPage,this.task.pageSize,this.task);
      },
      handleSizeChangeGroupAndPerson(val){
        this.groupAndPerson.pageSize=val;
        this.getDataFromTempGroupAndPerson(this.groupAndPerson.currentPage,this.groupAndPerson.pageSize,this.groupAndPerson);
      },
      handleCurrentChangeTask(val){
        this.task.currentPage=val;
        this.getDataFromTempTask(this.task.currentPage,this.task.pageSize,this.task);
      },
      lookMyInfor(){
        this.myInforFlag=true
      },
      lookDiscussGroup(){
        this.getDataFromTempGroup(1,10,this.discussGroup);
        this.discussGroup.discussGroupFlag=true;
        //this.discussGroup.totalCount=this.discussGroup.tableData.length;
      },
      lookTask(){
        this.getDataFromTempTask(1,10,this.task);
        this.task.taskFlag=true;
      },
      lookGroupAndPerson() {
        this.getDataFromTempGroupAndPerson(1,10,this.groupAndPerson);
        this.groupAndPerson.groupAndPersonFlag=true;
      },
      searchGroupName(){
        this.getDataFromTempGroup(this.discussGroup.currentPage,this.discussGroup.pageSize,this.discussGroup);
      },
      searchTaskName(){
        this.getDataFromTempTask(this.discussGroup.currentPage,this.discussGroup.pageSize,this.discussGroup);
      },
      getDataFromTempGroup(page,size,objName){
        //初始化数据
        objName.tableData =
          objName.tableDataTemp.filter(item=>item.groupName.indexOf(objName.condition) != -1 );
        objName.totalCount = objName.tableData.length;
        var start = ( objName.currentPage -1 )* objName.pageSize;
        objName.tableData = objName.tableData.slice(start,start + objName.pageSize);
      },
      getDataFromTempTask(page,size,objName){
        //初始化数据
        objName.tableData =
          objName.tableDataTemp.filter(item=>item.taskName.indexOf(objName.condition) != -1 );
        objName.totalCount = objName.tableData.length;
        var start = ( objName.currentPage -1 )* objName.pageSize;
        objName.tableData = objName.tableData.slice(start,start + objName.pageSize);
      },
      getDataFromTempGroupAndPerson(page,size,objName){
        //初始化数据
       /* objName.tableData =
          objName.tableDataTemp.filter(item=>item.taskName.indexOf(objName.condition) != -1 );*/
        objName.totalCount = objName.tableDataTemp.length;
        var start = ( objName.currentPage -1 )* objName.pageSize;
        objName.tableData = objName.tableDataTemp.slice(start,start + objName.pageSize);
      }
    }
  }
</script>

<style scoped>
  .el-pagination{
    float: right;
    margin: 5px 10px 10px auto;
  }
  .app-container{
    padding:0px;
    width: 100%;
    height: 100%;
  }
  .head:after,clear_left:after{
    content: "";
    clear: left;
    display: block;
  }
  .clear_right:after{
    content: "";
    clear: right;
    display: block;
  }

  .head > div{
    float: left;
    width: 24%;
    /*height: 120px;*/
    height:calc(20vh);

    margin:5px;
    position: relative;
  }
  .head > div:nth-child(1){
    background-color: #00C0EF;
  }
  .head > div:nth-child(2){
    background-color: #00A65A;
  }
  .head > div:nth-child(3){
    background-color: #F39C12;
  }
  .head > div:nth-child(4){
    background-color: #DD4B39;
  }
  .head .info,.infoEnglish{
    margin-left:10px;
    margin-top:10px;
    color: #fff;
  }
.info span:nth-child(1){
  color: #fff;
  font-size: 30px;
  font-weight: 800;
  }
  .info span:nth-child(2){
  margin: 10px;
  color: #000;
  font-size: 18px;
  font-weight: 600;
  }
  .moreInfor{
    color: #f9f9f9;
    position:absolute;
    bottom:0px;
    width: 100%;
    height: 20px;
    font-size: 15px;
    text-align: center;
    background:rgba(0,0,0,0.1);
  }
  .moreInfor:hover{
    cursor: pointer;
  }
  .content{
    height:calc(105vh);
    width:99%;
    margin:0px auto;
  }
  /**/
  /*.content{


    height:100%;
  }*/
  .el-dialog__header {
    padding: 10px 20px 0px;
  }

</style>
<style>
  .el-dialog__body{
    padding: 0px 20px 10px;
  }
</style>
