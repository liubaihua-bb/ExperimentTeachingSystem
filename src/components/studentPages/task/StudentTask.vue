<template>
  <div id="Task">
      <el-tabs class="stuTaskTab" v-model="activeName" @click="handleClick">

        <el-tab-pane name="project">
          <span slot="label" class="paneName"><i class="el-icon-date"></i> 实验项目</span>
          <StudentProject v-bind:course_id="course_ID"></StudentProject>
        </el-tab-pane>

        <el-tab-pane name="attendance">
          <span slot="label" class="paneName"><i class="el-icon-location-outline"></i> 考勤</span>
          <StudentAttendance v-bind:course_id="course_ID"></StudentAttendance>
        </el-tab-pane>
      </el-tabs>
  </div>
</template>

<script>
import StudentProject from "@/components/studentPages/task/StudentProject";
import StudentAttendance from "@/components/studentPages/task/StudentAttendance";

export default {
  name: "StudentTask",
  components:{
    StudentProject,
    StudentAttendance,
  },
  data(){
    return{
      activeName: 'project',
      course_ID: this.$route.params.course_id,
    }
  },
  methods:{
    handleClick(tab, event){
      console.log(tab, event);
    },
  },
}
</script>

<style scoped>
#Task{
  height: 100%;
  margin-top: 30px;
  margin-left: 250px;
  margin-right: 20px;
  background-color:white;
  cursor: context-menu;
}
.stuTaskTab{
  height: 100%;
  margin:30px 20px;
}
.paneName{
  height: 100%;
  margin: auto 120px;
  font-size: 17px;
}
</style>