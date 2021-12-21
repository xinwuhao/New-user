<template>
  <div class="container">
    <div class="content">
      <h4>新增用户</h4>
      <div class="flex">
        <el-button
          type="primary"
          icon="el-icon-plus"
          @click="dialogVisible = true"
          >新增用户</el-button
        >
        <div style="margin-left: 15px">
          <el-input
            placeholder="请输入内容"
            v-model="input"
            @input="seek(list, input)"
          >
            <el-button
              slot="append"
              icon="el-icon-search"
              @click="search(list, input)"
            ></el-button>
          </el-input>
        </div>
      </div>
      <!-- 用户列表 -->
      <div>
        <el-table :data="arr" border style="width: 100%">
          <el-table-column prop="name" label="姓名"> </el-table-column>
          <el-table-column prop="sex" label="性别"> </el-table-column>
          <el-table-column prop="contact" label="联系方式"> </el-table-column>
          <el-table-column prop="mailbox" label="邮箱"> </el-table-column>
          <el-table-column label="操作">
            <template slot-scope="scope">
              <el-button size="mini" @click="Edit(scope.$index, scope.row)"
                >编辑</el-button
              >
              <el-button size="mini" type="danger" @click="Delete(scope.row)"
                >删除</el-button
              >
            </template>
          </el-table-column>
        </el-table>
      </div>
      <!-- 新增内容弹出层 -->
      <el-dialog title="提示" :visible.sync="dialogVisible" width="30%">
        <el-form
          :model="ruleForm"
          :rules="rules"
          ref="ruleForm"
          label-width="100px"
          class="demo-ruleForm"
        >
          <el-form-item label="名称" prop="name">
            <el-input v-model="ruleForm.name"></el-input>
          </el-form-item>
          <el-form-item label="性别" prop="sex">
            <el-radio-group
              v-model="ruleForm.sex"
              v-for="(item, index) in sex"
              :key="index"
            >
              <el-radio :label="item" style="margin-right: 10px"></el-radio>
            </el-radio-group>
          </el-form-item>
          <el-form-item label="手机号码" prop="contact">
            <el-input v-model="ruleForm.contact"></el-input>
          </el-form-item>
          <el-form-item label="邮箱" prop="mailbox">
            <el-input v-model="ruleForm.mailbox"></el-input>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="submitForm('ruleForm')"
              >
              <div v-if="edit">立即新增</div>
              <div>修改</div>
              </el-button
            >
            <el-button @click="resetForm('ruleForm')">取消</el-button>
          </el-form-item>
        </el-form>
      </el-dialog>
    </div>
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
      edit: false,
      id: "",
      input: "",
      list: [
        {
          name: "张三",
          sex: "男",
          contact: "18581784400",
          mailbox: "12345@qq.com",
        },
        {
          name: "李四",
          sex: "女",
          contact: "18581784401",
          mailbox: "12346@qq.com",
        },
        {
          name: "赵五",
          sex: "隐藏",
          contact: "18581784402",
          mailbox: "12347@qq.com",
        },
      ],
      arr: [],
      sex: ["隐藏", "男", "女"],
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
          {
            pattern:
              /^(?:(?:\+|00)86)?1(?:(?:3[\d])|(?:4[5-79])|(?:5[0-35-9])|(?:6[5-7])|(?:7[0-8])|(?:8[\d])|(?:9[189]))\d{8}$/,
            message: "输入的手机号码有误",
            trigger: "blur",
          },
        ],
        mailbox: [
          { required: true, message: "请输入邮箱", trigger: "blur" },
          {
            pattern:
              /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/,
            message: "输入的邮箱有误",
            trigger: "blur",
          },
        ],
        sex: [{ required: true, message: "性别", trigger: "change" }],
      },
    };
  },
  components: {},
  methods: {
    //表单创建按钮
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          this.dialogVisible = false;
          if (this.edit == false) {
            this.$message.success("新增成功");
            this.list.unshift(this.ruleForm);
          } else {
            this.$message.success("修改成功");
            this.list.map((item, index) => {
              if (this.id == index) {
                // console.log(item, this.ruleForm);
                item = this.ruleForm;
              }
            });
          }
          this.edit = false;
          console.log(this.list);
        } else {
          this.$message.error("您还有信息没有填写或者填写的信息有误");
          return false;
        }
      });
    },
    //表单取消按钮
    resetForm(formName) {
      this.$refs[formName].resetFields();
      this.dialogVisible = false;
    },
    //搜索
    search(list, e) {
      let reg = new RegExp(e);
      this.arr = [];
      for (let i = 0; i < list.length; i++) {
        if (reg.test(list[i].name)) {
          this.arr.push(list[i]);
        }
      }
    },
    seek(list, e) {
      let reg = new RegExp(e);
      this.arr = [];
      for (let i = 0; i < list.length; i++) {
        if (reg.test(list[i].name)) {
          this.arr.push(list[i]);
        }
      }
      console.log(this.arr);
    },
    //编辑
    Edit(index, row) {
      this.dialogVisible = true;
      this.ruleForm = row;
      this.edit = true;
      this.id = index;
      console.log(this.id);
    },
    //删除
    Delete(index, row) {
      console.log(index, row);
    },
  },
  mounted() {
    this.arr = this.list;
  },
  computed: {},
  watch: {},
};
</script>

<style lang='scss' scoped>
.container {
  display: flex;
  justify-content: center;
}
.content {
  width: 1450px;
  /* 注意适配的宽度必须大于最小适配宽度 */
}
.flex {
  display: flex;
  margin-bottom: 15px;
}
</style>