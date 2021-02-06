<template>
    <div style="width: 100%;height: 100%;">
      <!--<iframe src="../../../static/bigscreem/statisticdetail/statistic.html"
              frameborder="0" height="100%" width="100%"></iframe>-->
      <!--<iframe src="../../../static/bigscreem/statisticdetail/statistic1.html"
              frameborder="0" height="100%" width="100%"></iframe>-->
     <!-- <iframe src="../../../static/bigscreem/statisticdetail/statistic2.html"
                    frameborder="0" height="100%" width="100%"></iframe>-->
      <table-demo></table-demo>
    </div>
</template>

<script>
  import tableDemo from '../../views/tableDemo/index'
    export default {
      components:{
        tableDemo
      },
        name: "StatisticDetail"
    }
</script>

<style scoped>
  /*.table-demo{
    height:100%;
    width:100%;
  }*/

</style>
