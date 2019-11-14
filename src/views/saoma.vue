<template>
  <div id="main">
    <DoctorHeader :department="department" :name="name"></DoctorHeader>
    <div class="main_content">
      <div class="patient">
        <div class="pname">王小二</div>
        <div class="pname">男</div>
        <div class="pname">34岁</div>
      </div>
      <div class="saoma">
        <div>
          <a-input class="ainput" placeholder="请先扫获取患者授权，查询患者最近三次历史就诊记录" />
        </div>
        <div class="pname">
          <a-button type="primary">扫码</a-button>
        </div>
        <div class="pname">
          <a-button type="primary">录入诊断</a-button>
        </div>
      </div>
      <div class="recent bg">
        <div class="incontent bg2">
          <a-card
            title
            :bordered="true"
            class="css1"
            v-for="(checks,index) in tableData"
            :key="index"
          >
            <div>
              <div class="text">项目名称：</div>
            </div>
            <div>
              <div class="text">检查科室：/div>
            </div>
            <div>
              <div class="text">检查时间：</div>
            </div>
          </a-card>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import DoctorHeader from "@/components/header/doc-header";
export default {
  components: { DoctorHeader },
  data() {
    return {
      name: "",
      department: ""
    };
  },
  created() {
    this.getDoctorAndPatients();
  },
  computed: {
    // whichcolor: function() {
    //   alert(this.patients.name);
    //   if (this.patients.length == 1) {
    //     return "1";
    //   }
    //   return "patient";
    // }
  },
  watch: {
    // patients: {
    //   handler(newValue, oldValue) {
    //     for (let i = 0; i < newValue.length; i++) {
    //       if (oldValue[i] != newValue[i]) {
    //         window.console.log(newValue);
    //       }
    //     }
    //   },
    //   deep: true
    // }
  },
  methods: {
    getDoctorAndPatients() {
      this.$ajax
        .get("api/v1/doctor1")
        .then(res => {
          window.console.log(res);
          this.department = res.data.department;
          this.name = res.data.doctorName;
        })
        .catch(res => {
          window.console.log(res);
        });
    }
  }
};
</script>
<style lang="less" scoped>
.bg {
  background-color: aqua;
}
.bg2 {
  background-color: rgb(214, 90, 177);
}
#main {
  width: 100%;
  min-height: 100%;
  background: rgba(240, 242, 245, 1);
  background: #f0f2f5;
  flex-direction: column;
  .main_content {
    flex-direction: column;
    .patient {
      width: 100%;
      height: 60px;
      display: flex;
      justify-content: center;
      align-items: center;
      .pname {
        height: 33px;
        width: 100px;
        font-size: 24px;
        font-family: PingFangSC-Regular, PingFang SC;
        font-weight: 400;
        color: rgba(51, 51, 51, 1);
        line-height: 33px;
        text-align: left;
      }
    }
    .saoma {
      width: 100%;
      height: 60px;
      display: flex;
      justify-content: center;
      align-items: center;
      .ainput {
        width: 600px;
      }
      .pname {
        width: 100px;
      }
    }
    .recent {
      width: 100%;
      height: 60px;
      display: flex;
      justify-content: center;
      align-items: center;
      .incontent {
        width: 1000px;
      }
    }
  }
}
.main_p1 {
  width: 10px;
}
.a1 {
  width: 100px;
}
.main_content {
  margin: 18px;
  display: flex;
  flex-direction: row;
}
</style>
