<template>
  <div>
    <div class="projectCard" v-for="project in project_list">
      <el-descriptions :title="project.name" :column="2">
        <template slot="extra">
          <el-button type="primary" icon="el-icon-edit" plain id="checkButton" size="medium" @click="btnClick(project.start_time,project.name)">去完成</el-button>
        </template>
        <el-descriptions-item label="开始时间">{{project.start_time}}</el-descriptions-item>
        <el-descriptions-item label="截止时间" id="redEndTime">{{project.end_time}}</el-descriptions-item>
        <el-descriptions-item label="发布老师">{{project.teacher_name}}</el-descriptions-item>
      </el-descriptions>
      <el-divider></el-divider>
    </div>
  </div>
</template>

<script>

import router from "@/router";

export default {
  name: "StudentProject",
  props:{
    course_id:{
      type: String,
      default: '',
    },
  },
  data(){
    return{
      project_list:[],
    }
  },
  methods:{
    btnClick(start_time, name){
      var moment=require('moment');
      // 格式化
      if(start_time > moment(new Date()).format('YYYY-MM-DD HH:mm:ss')){
        this.$message({
          message: '项目还未发布，暂时无法查看',
          type: 'warning'
        });
      }
      else{
        console.log(this.course_id);
        console.log(name);
        router.push({name: 'stuProjectInfo',
          params: {
          course_ID: this.course_id,
            name: name,
          }});
      }
    },
  },
  mounted() {
    let _this=this
    let id = _this.course_id
    // window.alert(id);
    this.$axios.get(
        '/project/getProjectInfoListByCourseId',{
          params: {
            course_ID: id,
          },
        })
        .then((response)=>{
          _this.project_list=response.data
        })
  }
}
</script>

<style scoped>
.projectCard{
  margin-top: 30px;
  margin-left: 50px;
  margin-right: 50px;
  cursor: context-menu;
}

#redEndTime{
  color: tomato;
}
</style>