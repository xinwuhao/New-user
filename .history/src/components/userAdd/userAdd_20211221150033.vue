<template>
  <div>
    <el-button type="primary" icon="el-icon-plus" @click="dialogVisible = true"
      >新增用户</el-button
    >
    <el-dialog title="提示" :visible.sync="dialogVisible" width="30%">
    
    </el-dialog>
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
    };
  },
  components: {},
  methods: {},
  mounted() {},
  computed: {},
  watch: {},
};
</script>

<style lang='scss' scoped>
</style>