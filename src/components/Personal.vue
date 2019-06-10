<template>
    <div id="personal" v-loading="loading">
      <!--上面导航栏-->
      <el-header style="background-color: #eff4fa;">
        <div>
          <el-menu :default-active="activeIndex" class="el-menu-demo"  mode="horizontal" @select="handleSelect" style="background-color:#eff4fa;border-bottom: 0;">
            <el-menu-item index="1" style="float:right">返回首页</el-menu-item>
            <el-menu-item index="2" style="float:right">意见反馈</el-menu-item>
            <el-submenu index="3" style="float:right">
              <template slot="title" >语言</template>
              <el-menu-item index="2-1">简体中文</el-menu-item>
              <el-menu-item index="2-2">繁体中文</el-menu-item>
              <el-menu-item index="2-3">English</el-menu-item>
            </el-submenu>
            <el-menu-item index="4" style="float:left"><img src="https://dummyimage.com/130x50/000/fff" alt="aaa"></el-menu-item>
          </el-menu>
        </div>
      </el-header>

      <!--左边导航连-->
      <el-aside style="width:20%;margin-top: 40px; margin-left: 20px; float: left" >
        <div style=" margin-left: 5%">
          <div class="info_edit" >
            <el-row>
              <el-col :span="6" :offset="1">
                <el-progress type="circle" :percentage="25" width="100"></el-progress>
              </el-col>
              <el-col :span="3"><div class="grid-content bg-white"></div></el-col>
              <el-col :span="12" style="margin-top:1%">
                个人资料完成度<span class="percent">25%</span>
                <div style="margin-top: 15px">
                  <el-button type="primary" icon="el-icon-edit" size="small" style="margin-right: 10px"></el-button>去编辑个人信息
                </div>
              </el-col>
            </el-row>
          </div>
          <div class="photos">
            <div class="photos-header">
              相册
            </div>
            <div class="separate"></div>
            <div style="margin: 0 5px;">
              <div class="photos-pre">
                <img src="https://dummyimage.com/344x500/054/fff" alt="" style="width: 100%;height: 100%;">
              </div>
            </div>
            <div class="separate"></div>
            <div class="photos-seemore">
              <a href="#">查看更多 ></a>
            </div>
          </div>
        </div>
      </el-aside>

      <!--主模块-->
      <el-main class="main">
        <!--名片-->
        <div>
        <el-row>
          <el-col :span="15" offset="7">
            <div class="profile" >
              <div class="avatar">
                <el-upload
                  class="avatar-uploader"
                  action="https://jsonplaceholder.typicode.com/posts/"
                  :show-file-list="false"
                  :on-success="handleAvatarSuccess"
                  :before-upload="beforeAvatarUpload">
                  <img v-if="imageUrl" :src="imageUrl" class="avatar" alt="">
                  <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                </el-upload>
              </div>
              <div class="user_name">
                username
              </div>
              <div class="description">
                编辑你的个人资料
              </div>
            </div>
          </el-col>
          <el-col :span="17" offset="2">
            <div class="option" >
              <el-tabs v-model="activeName" @tab-click="handleClick" stretch="true">
                <el-tab-pane label="我的日志" name="first" ></el-tab-pane>
                <el-tab-pane label="我的留言" name="second"></el-tab-pane>
                <el-tab-pane label="编辑资料" name="third"></el-tab-pane>
              </el-tabs>
            </div>
          </el-col>
          <el-col v-if="activeName==='third'" offset="2" span="17">
            <EditInformation />
          </el-col>
        </el-row>
        <!--上方导航栏-->
        </div>
      </el-main>


      <!--页脚-->
      <el-footer height="90px" style="background-color: #eff4fa;">
        <div style="margin-left:405px;display:inline-block;position: relative;top:40px" >
          <el-breadcrumb separator="|">
            <el-breadcrumb-item><a href="/">关于我们</a></el-breadcrumb-item>
            <el-breadcrumb-item><a href="/">用户条约</a></el-breadcrumb-item>
            <el-breadcrumb-item><a href="/">帮助中心</a></el-breadcrumb-item>
            <el-breadcrumb-item><a href="/">隐私政策</a></el-breadcrumb-item>
            <el-breadcrumb-item>2018 STU version:1.0.0 / all rights reserved </el-breadcrumb-item>
          </el-breadcrumb>
        </div>
      </el-footer>

    </div>
</template>

<script>
import EditInformation from './EditInformation'
var activeName
export default {
  name: 'Personal',
  components: {EditInformation},
  data () {
    return {
      loading:false,
      activeName: '',
      imageUrl: 'https://dummyimage.com/100x100/00f/fff'
    }
  },
  methods: {
    handleClick (tab, event) {
      switch (tab) {
        case "我的日志": activeName="first";break;
        case "我的留言": activeName="second";break;
        case "编辑资料": activeName="third";break;
        default: activeName="first"
      }
    },
    handleAvatarSuccess (res, file) {
      this.imageUrl = URL.createObjectURL(file.raw)
    },
    beforeAvatarUpload (file) {
      const isJPG = file.type === './assets/bg.jpg'
      const isLt2M = file.size / 1024 / 1024 < 2

      if (!isJPG) {
        this.$message.error('上传头像图片只能是 JPG 格式!')
      }
      if (!isLt2M) {
        this.$message.error('上传头像图片大小不能超过 2MB!')
      }
      return isJPG && isLt2M
    }
  }
}
</script>

<style scoped>
  #personal {
    /*background-image: url(../assets/bg.jpg);*/
    background-color: rosybrown;
    background-attachment: fixed;
    background-size: 100% 100%;

  }
  .option {
     background: white;
   }
  .photos-seemore{
    text-align: center;
    padding: 10px;
  }
  .photos-seemore a{
    text-decoration-line: none;
    color: black;

  }
  .photos-seemore a:hover{
    color: rgb(253, 152, 0)
  }
  .el-row{
    margin-bottom:0 !important;
  }
  .user_name{
    margin: 20px 0;
  }
  .info_edit {
    padding: 10px 0;
    background-color: white;
    border-radius: 5px;
  }
  .photos{
    margin:10px 0;
    background-color: white;
    border-radius: 5px;
  }
  .photos-header{
    padding-top:10px;
    margin-left: 10px;
    font-weight: 700;

  }
  .info_edit .percent {
    color: rgb(0, 174, 255);
    font-size: 30px;
  }
  div.avatar{
    padding-top:35px;
    margin: 0 auto;
    width: 100px;
    height: 100px;
  }

  div.avatar *{
    width: 100px;
    height: 100px;
    border: 0 !important;
    padding: 0 !important;
    margin: 0 !important;
  }

  .profile *{
    color: white;
    text-align: center;
  }
  .profile{
    background-image: url(https://dummyimage.com/997x300/000/fff);
    width:997px;
    height:300px;
  }
  .separate{
    height: 1px;
    margin: 5px 0;
    border-top: 1px solid #ddd;
    text-align: center;
  }
  body {
    margin:0;
  }

  .el-row {
    margin-bottom: 20px;
  &:last-child {
     margin-bottom: 0;
   }
  }
  .el-col {
    border-radius: 4px;
  }
  .bg-purple-dark {
    background: #99a9bf;
  }
  .bg-white {
    background: white;
  }
  .bg-purple {
    background: #d3dce6;
  }
  .bg-purple-light {
    background: #e5e9f2;
  }
  .grid-content {
    border-radius: 4px;
    min-height: 36px;
  }
  .row-bg {
    padding: 10px 0;
    background-color: #f9fafc;
  }
  .el-carousel__item h3 {
    color: #475669;
    font-size: 18px;
    opacity: 0.75;
    line-height: 300px;
    margin: 0;
  }

  .el-carousel__item:nth-child(2n) {
    background-color: #99a9bf;
  }

  .el-carousel__item:nth-child(2n+1) {
    background-color: #d3dce6;
  }

</style>
