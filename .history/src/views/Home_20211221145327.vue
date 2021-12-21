<template>
  <div class="container">
    <div class="content">
      <h4>新增用户</h4>
      <div>
        <el-button type="primary" icon="el-icon-plus" @click="userAdd">新增用户</el-button>
      </div>
    </div>
  </div>
</template>
 
<script>
//引入子组件
import userAdd 
export default {
  name: "",
  props: {},
  data() {
    return {};
  },
  components: {},
  methods: {
    userAdd(){
      console.log(123)
    }
  },
  mounted() {},
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
</style>