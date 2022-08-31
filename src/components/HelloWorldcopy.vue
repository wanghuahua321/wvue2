<template>
  <el-tree
    :data="dataTree"
    :props="defaultProps"
    node-key="id"
    highlight-current
    ref="dataConfigTree"
    :expand-on-click-node="false"
    accordion
    show-checkbox
    nodeChange.isLeaf="true"
    :filter-node-method="filterNode"
    @check="getname"
    :default-checked-keys="checkIdList"
    :default-expanded-keys="expandedList"
  >
  </el-tree>
</template>
<script>
export default {
  data() {
    return {
      dataTree: [{ children: [] }],
      defaultProps: {
        children: 'children',
        label: 'label'
      },
      checkIdList: [], //默认勾选三级
      expandedList: [] //展开项
    };
  },
  methods: {
    handleNodeClick(data) {
      console.log(data);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* :deep(.el-checkbox) {
  display: flex !important;
} */
</style>
