<template>
  <div class="h1">
    <div class="reg_h1">
      <div class="login_h9"></div>
      <div class="reg_h2">
        <div class="reg_h3">欢迎注册</div>
        <div class="login_h4">
          <div for="name">用户名</div>
          <input
            id="name"
            v-decorator="[
          'user.name',
          { rules: [{ required: true, message: 'Please input your name' }] },
        ]"
            type="text"
            placeholder="请输入用户名"
            v-model="user.name"
          />
          <br />
          <div for="idcard" style="margin-top:20px">身份证号码</div>
          <input id="idcard" type="text" placeholder="请输入身份证号码" v-model="user.idcard" />
          <br />
          <div for="password" style="margin-top:20px">设置密码</div>
          <input id="password" type="text" placeholder="请输入密码" v-model="user.password" />
          <br />
          <div for="aa" style="margin-top:20px">短信验证码</div>
          <input id="aa" type="text" placeholder="请输入密码" v-model="user.aa" style="width:390px" />
          <a-button class="login_h7" type="primary">获取验证码</a-button>
          <br />
          <div for="certificate" style="margin-top:20px">职业资格证编号</div>
          <input id="certificate " type="text" placeholder="请输入密码" v-model="user.certificate " />
          <span class="login_h8">请补全医生信息</span>
          <br />
          <div for="grade" style="margin-top:20px">级别</div>
          <a-select style="width: 500px" v-model="user.grade">
            <a-select-option value="主任医师">主任医师</a-select-option>
            <a-select-option value="副主任医师">副主任医师</a-select-option>
            <a-select-option value="主治医师">主治医师</a-select-option>
          </a-select>
          <br />
          <div for="department" style="margin-top:20px">科室名称</div>
          <input id="department " type="text" placeholder="请科室名称" v-model="user.department " />
          <div for="location" style="margin-top:20px">问诊地点</div>
          <input id="location " type="text" placeholder="请问诊地点" v-model="user.location " />
          <div class="login_h5">
            <div class="login_h6"></div>
            <a-button class="login_h7" type="primary" @click="regDoc">确定</a-button>
            <div class="login_h6"></div>
            <div class="login_h6"></div>
            <a-button
              class="login_h7"
              style="border:1px solid #0090FF;color:#0090FF"
              @click="goback"
            >返回</a-button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      user: {
        name: "",
        idcard: "",
        mobile: "",
        password: "",
        certificate: "",
        department: "",
        location: "",
        grade: "主任医师",
        roles: "1"
      },
      name: "ss",
      tipinfo: ""
    };
  },
  methods: {
    goback() {
      this.$router.push("/login");
    },
    regDoc() {
      window.console.log(this.user);
      this.$ajax
        .put("/api/v1/user", this.user)
        .then(res => {
          window.console.log(res);
          this.tipinfo = res.data.message;
          this.success();
        })
        .catch(res => {
          window.console.log(res);
        });
    },
    success() {
      this.$success({
        title: "成功提示",
        // JSX support
        content: this.tipinfo
      });
    }
  }
};
</script>
<style lang="less" scoped>
.bg {
  background-color: aquamarine;
}
.bg1 {
  background-color: sandybrown;
}
.h1 {
  background-image: url("../assets/l1.png");
  background-size: 100% 100%;
  width: 100%;
  display: flex;
  flex-direction: row; /* 子元素横向排列 */
  justify-content: center; /* 相对父元素水平居中 */
  align-items: center; /*  子元素相对父元素垂直居中 */
}
.reg_h1 {
  margin-top: 50px;
  margin-bottom: 50px;
  width: 1000px;
  height: 1120px;
  background: rgba(255, 255, 255, 1);
  box-shadow: 0px 3px 18px 0px rgba(21, 24, 113, 1);
  border-radius: 18px;
  display: flex;
  justify-content: center;
}
.reg_h2 {
  margin-top: 30px;
  margin-bottom: 30px;
  margin-left: 50px;
  width: 700px;
  text-align: left;
}
.reg_h3 {
  height: 56px;
  font-size: 30px;
  font-family: PingFangSC-Semibold, PingFang SC;
  font-weight: 600;
  color: rgba(51, 51, 51, 1);
  line-height: 56px;
  margin-bottom: 30px;
}
.login_h4 {
  height: 40px;
  font-size: 20px;
  font-family: PingFangSC-Semibold, PingFang SC;
  font-weight: 600;
  color: rgba(51, 51, 51, 1);
  line-height: 40px;
}
.login_h5 {
  height: 100px;
  display: flex;
  align-items: center;
}
.login_h6 {
  width: 20px;
}
input {
  outline: none;
  border: none;
  border-bottom: 1px solid #d8d8d8;
  padding: 7px 0;
  color: #999999;
  font-size: 14px;
  font-weight: 400;
  width: 500px;
}
.login_h7 {
  width: 150px;
  height: 40px;
}
.login_h8 {
  font-size: 16px;
  font-family: PingFangSC-Regular, PingFang SC;
  font-weight: 400;
  color: rgba(255, 91, 91, 1);
}
.login_h9 {
  width: 100px;
}
</style>