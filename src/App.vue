<template>
  <div id="app">
    <div class="col-9 offset-2">
      <table class="table caption-top table-hover">
        <caption class="text-center">
          <h1>学生信息管理系统</h1>
          <el-button type="primary" @click="getStudents">获取学生信息</el-button>
          <el-button type="warning" @click="dialogVisible = true">添加学生</el-button>
          <el-input type="text" placeholder="请输入姓名" class="w-25" v-model="search_name" /><el-button type="success"
            @click="search">搜索</el-button>
          <el-dialog class="bootstrap-dialog" title="提示" :visible.sync="dialogVisible" width="30%"
            :before-close="handleClose">
            <div class="bootstrap-dialog-header bg-primary text-white p-3">添加学生信息</div>
            <el-form class="bootstrap-form">
              <el-row>
                <el-col :span="6">
                  <el-form-item label="学号">
                    <el-input class="bootstrap-input" v-model="newStudent.studentId"></el-input>
                  </el-form-item>
                </el-col>
                <el-col :span="6">
                  <el-form-item label="姓名">
                    <el-input class="bootstrap-input" v-model="newStudent.name"></el-input>
                  </el-form-item>
                </el-col>
                <el-col :span="6">
                  <el-form-item label="性别">
                    <el-input class="bootstrap-input" v-model="newStudent.gender"></el-input>
                  </el-form-item>
                </el-col>
                <el-col :span="6">
                  <el-form-item label="电话号码">
                    <el-input class="bootstrap-input" v-model="newStudent.phoneNumber"></el-input>
                  </el-form-item>
                </el-col>
              </el-row>
              <el-row>
                <el-col :span="6">
                  <el-form-item label="邮箱">
                    <el-input class="bootstrap-input" v-model="newStudent.email"></el-input>
                  </el-form-item>
                </el-col>
                <el-col :span="6">
                  <el-form-item label="家庭地址">
                    <el-input class="bootstrap-input" v-model="newStudent.address"></el-input>
                  </el-form-item>
                </el-col>
                <el-col :span="6">
                  <el-form-item label="班级">
                    <el-input class="bootstrap-input" v-model="newStudent.className"></el-input>
                  </el-form-item>
                </el-col>
                <el-col :span="6">
                  <el-form-item label="年级">
                    <el-input class="bootstrap-input" v-model="newStudent.grade"></el-input>
                  </el-form-item>
                </el-col>
              </el-row>
              <el-row>
                <el-col :span="6">
                  <el-form-item label="专业">
                    <el-input class="bootstrap-input" v-model="newStudent.major"></el-input>
                  </el-form-item>
                </el-col>
                <el-col :span="6">
                  <el-form-item label="辅导员">
                    <el-input class="bootstrap-input" v-model="newStudent.counselor"></el-input>
                  </el-form-item>
                </el-col>
              </el-row>
            </el-form>
            <span slot="footer" class="dialog-footer bootstrap-dialog-footer">
              <el-button class="bootstrap-button" @click="dialogVisible = false">取 消</el-button>
              <el-button class="bootstrap-button-primary" type="primary" @click="addStudent">添加</el-button>
            </span>
          </el-dialog>
          <el-button type="info" class="el-button--info btn btn-primary btn-lg"
            @click="dialogVisiblelogin = true">登录</el-button>
          <el-dialog title="提示" :visible.sync="dialogVisiblelogin" width="30%" :before-close="handleClose"
            class="bootstrap-dialog">
            <div class="el-form-item">
              <label class="el-form-item__label text-primary">用户名</label>
              <div class="el-form-item__content">
                <input type="text" class="el-input__inner form-control" v-model="user_for_login.username">
              </div>
            </div>
            <div class="el-form-item">
              <label class="el-form-item__label text-primary">密码</label>
              <div class="el-form-item__content">
                <input type="password" class="el-input__inner form-control" v-model="user_for_login.password">
              </div>
            </div>
            <span slot="footer" class="dialog-footer">
              <el-button @click="dialogVisiblelogin = false" class="btn btn-secondary">取消</el-button>
              <el-button type="primary" @click="login" class="btn btn-success">登录</el-button>
            </span>
          </el-dialog>
          <el-button type="danger" class="el-button--danger btn btn-danger"
            @click="dialogVisibleregister = true">注册</el-button>
          <el-dialog title="提示" :visible.sync="dialogVisibleregister" width="30%" :before-close="handleClose"
            class="bootstrap-dialog">
            <div class="el-form-item">
              <label class="el-form-item__label text-danger">用户名</label>
              <div class="el-form-item__content">
                <input type="text" class="el-input__inner form-control" v-model="user_for_register.username">
              </div>
            </div>
            <div class="el-form-item">
              <label class="el-form-item__label text-danger">密码</label>
              <div class="el-form-item__content">
                <input type="password" class="el-input__inner form-control" v-model="user_for_register.password">
              </div>
            </div>
            <div class="el-form-item">
              <label class="el-form-item__label text-danger">确认密码</label>
              <div class="el-form-item__content">
                <input type="password" class="el-input__inner form-control" v-model="user_for_register.confirmPassword">
              </div>
            </div>
            <span slot="footer" class="dialog-footer">
              <el-button @click="dialogVisibleregister = false" class="btn btn-secondary">取消</el-button>
              <el-button type="primary" @click="register" class="btn btn-success">注册</el-button>
            </span>
          </el-dialog>

        </caption>
        <thead>
          <tr class="table-primary">
            <th scope="col">学号</th>
            <th scope="col">姓名</th>
            <th scope="col">性别</th>
            <th scope="col">电话号码</th>
            <th scope="col">邮箱</th>
            <th scope="col">家庭地址</th>
            <th scope="col">班级</th>
            <th scope="col">年级</th>
            <th scope="col">专业</th>
            <th scope="col">辅导员</th>
            <th scope="col">操作</th>
          </tr>

        </thead>
        <tbody>
          <Student v-for="stu in students_for_page" :key="stu.id" :student="stu"></Student>
        </tbody>
      </table>
      <div class="text-center">
        <el-button-group>
          <el-button type="primary" icon="el-icon-arrow-left" @click="last_page">上一页</el-button>
          <el-button type="primary" @click="next_page">下一页<i class="el-icon-arrow-right el-icon--right"></i></el-button>
        </el-button-group>
      </div>
    </div>
  </div>
</template>

<script>
import Student from './components/Student.vue'
import axios from 'axios'
export default {
  page: 1,
  name: 'app',
  components: {
    Student
  },
  data() {
    return {
      search_name: "",
      user_for_login: {
        username: "",
        password: "",
      },
      user_for_register: {
        username: "",
        password: "",
        confirmPassword: ""
      },
      page: 1,
      students: [],
      dialogVisible: false,
      dialogVisiblelogin: false,
      dialogVisibleregister: false,
      newStudent: {
        studentId: "",
        name: "",
        gender: "",
        phoneNumber: "",
        email: "",
        address: "",
        className: "",
        grade: "",
        major: "",
        counselor: ""

      }
    }
  },
  methods: {
    next_page() {
      this.page += 1;
    },
    last_page() {
      this.page -= 1;
    },
    getStudents() {
      if (sessionStorage.getItem("isLogined") == "true") {
        axios({
          url: "http://localhost:8081/students",
          method: "GET",
        }).then(res => {
          console.log(res.data);
          this.students = res.data;
        })
      }
      else {
        this.$alert("请先登陆")
      }
    },
    handleClose(done) {
      this.$confirm('确认关闭？')
        .then(() => {
          done();
        })
        .catch(() => { });
    },
    addStudent() {
      axios({
        url: "http://localhost:8081/add",
        method: "POST",
        data: this.newStudent
      })
      this.dialogVisible = false
    },
    login() {
      axios({
        url: "http://localhost:8081/login",
        method: "POST",
        data: this.user_for_login
      }).then(res => {
        console.log(res.data);
        localStorage.setItem("login", res.data)
        if (res.data == "1") {
          sessionStorage.setItem("isLogined", "true");
        }
        else {
          alert("用户名或者密码错误")
        }
      })
      this.dialogVisiblelogin = false
    },
    register() {
      axios({
        url: "http://localhost:8081/register",
        method: "POST",
        data: this.user_for_register
      })
      this.dialogVisibleregister = false;
      this.$alert("注册成功")
    },
    search() {
      axios({
        url: "http://localhost:8081/search",
        method: "POST",
        data: {
          name: this.search_name
        }
      }).then(res => {
        this.students = res.data
      })
    }


  },
  computed: {
    students_for_page() {
      return this.students.slice(this.page * 5 - 5, this.page * 5);
    }
  }

}
</script>

<style></style>
