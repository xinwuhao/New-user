<template>
  <div>
    
  </div>
</template>
 
<script>
//引入子组件

export default {
  name: "",
  props: {},
  data() {
    return {
      dialogVisible: false,
      ruleForm: {
        name: "",
        sex: "",
        contact: "",
        mailbox: "",
      },
      rules: {
        name: [
          { required: true, message: "请输入用户名称", trigger: "blur" },
          { min: 1, max: 5, message: "长度在 1 到 5 个字符", trigger: "blur" },
        ],
        contact: [
          { required: true, message: "请输入手机号码", trigger: "blur" },
          { min: 11, max: 11, message: "输入的手机号码有误", trigger: "blur" },
        ],
        // mailbox: [
        // //   { required: true, message: "请输入用户名称", trigger: "blur" },
        // //   { min: 1, max: 5, message: "长度在 1 到 5 个字符", trigger: "blur" },
        // ],
        sex: [
          { required: true, message: "性别", trigger: "change" },
        ],
      },
    };
  },
  components: {},
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          this.$message.success("新增成功");
          this.dialogVisible = false;
        } else {
          this.$message.error("您还有信息没有填写或者填写的信息有误");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
      this.dialogVisible = false;
    },
  },
  mounted() {},
  computed: {},
  watch: {},
};
</script>

<style lang='scss' scoped>
</style>