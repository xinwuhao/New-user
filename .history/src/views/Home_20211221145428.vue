<template>
  <div class="container">
    <div class="content">
      <h4>新增用户</h4>
      <userAdd></userAdd>
    </div>
  </div>
</template>
 
<script>
//引入子组件
import userAdd from "../components/userAdd/userAdd.vue"
export default {
  name: "",
  props: {},
  data() {
    return {};
  },
  components: {
    userAdd
  },
  methods: {
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