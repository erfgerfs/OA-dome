<template>
  <div class="login-container">
    <div class="left">
      <img src="../../assets/common/login_back.png" alt="">
    </div>
    <div class="rigth">
      <h1 style="margin-left: 120px">手机号登录</h1>
      <el-form
        ref="ruleForm"
        :model="ruleForm"
        :rules="rules"
        label-width="100px"
        class="demo-ruleForm"
      >
        <el-form-item prop="phone">
          <el-input v-model="ruleForm.phone" placeholder="请输入手机号" />
        </el-form-item>
        <el-form-item prop="name">
          <el-input v-model="ruleForm.name" placeholder="请输入密码" />
        </el-form-item>
        <el-form-item prop="checked1">
          <el-checkbox v-model="ruleForm.checked1">用户平台使用协议</el-checkbox>
        </el-form-item>
        <el-form-item>
          <el-button
            type="primary"
            style="width: 340px"
            @click="submitForm('ruleForm')"
          >立即创建</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data() {
    return {
      ruleForm: {
        name: '',
        phone: '',
        checked1: false
      },
      rules: {
        phone: [
          { required: true, message: '请输入手机号', trigger: 'blur' },
          { pattern: /^1[3-9]\d{9}$/, message: '手机格式不正确', trigger: 'blur' }
        ],
        name: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 5, max: 11, message: '5-11', trigger: 'blur' }
        ],
        checked1: [
          {
            validator: (rule, value, callback) => {
              value ? callback() : callback(new Error('没有勾选用户平台协议'))
            }
          }
        ]
      }
    }
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert('submit!')
        } else {
          console.log('error submit!!')
          return false
        }
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.login-container {
  width: 100%;
  height: 100vh;
  // background-color: cadetblue;
  display: flex;

  .left {
    flex: 3;
    width: 100%;
    height: 100vh;

    img {
      width: 100%;
      height: 100%;
      border-top-right-radius: 100px;
    }
  }
  .rigth {
    flex: 2;
    display: flex;
    flex-direction: column;
    // text-align: center;

    justify-content: center;
    .demo-ruleForm {
      padding-left: 30px;
      margin-right: 120px;
    }
  }
}
</style>
