<template>
  <!-- <el-transfer v-model="checked" :data="transferData" filterable filter-placeholder="请输入城市拼音">
    <span slot-scope="{ option }"> {{ option.label }} === </span>
  </el-transfer> -->

  <tree-transfer
    :title="title"
    :from_data="fromData"
    :to_data="toData"
    :defaultProps="{ label: 'label' }"
    @add-btn="add"
    @remove-btn="remove"
    :mode="mode"
    height="540px"
    filter
    openAll
  >
  </tree-transfer>
</template>
<script>
import treeTransfer from 'el-tree-transfer';
export default {
  components: {
    treeTransfer
  },
  data() {
    return {
      // transferData: [
      //   {
      //     key: 1,
      //     label: 'huahua',
      //     disabled: false
      //   },
      //   {
      //     key: 2,
      //     label: 'huahua2',
      //     disabled: false
      //   },
      //   {
      //     key: 3,
      //     label: 'huahua2',
      //     disabled: false
      //   },
      //   {
      //     key: 4,
      //     label: 'huahua2',
      //     disabled: false
      //   }
      // ], // 总数据
      // checked: [] // 右侧所分配数组

      mode: 'transfer', // transfer addressList
      fromData: [
        {
          id: '1',
          pid: 0,
          label: '一级 1',
          children: [
            {
              id: '1-1',
              pid: '1',
              label: '二级 1-1',
              disabled: true,
              children: []
            },
            {
              id: '1-2',
              pid: '1',
              label: '二级 1-2',
              children: [
                {
                  id: '1-2-1',
                  pid: '1-2',
                  children: [],
                  label: '二级 1-2-1'
                },
                {
                  id: '1-2-2',
                  pid: '1-2',
                  children: [],
                  label: '二级 1-2-2'
                }
              ]
            }
          ]
        }
      ],
      toData: []
    };
  },
  methods: {
    // 切换模式 现有树形穿梭框模式transfer 和通讯录模式addressList
    changeMode() {
      if (this.mode == 'transfer') {
        this.mode = 'addressList';
      } else {
        this.mode = 'transfer';
      }
    },
    // 监听穿梭框组件添加
    add(fromData, toData, obj) {
      // 树形穿梭框模式transfer时，返回参数为左侧树移动后数据、右侧树移动后数据、移动的{keys,nodes,halfKeys,halfNodes}对象
      // 通讯录模式addressList时，返回参数为右侧收件人列表、右侧抄送人列表、右侧密送人列表
      console.log('fromData:', fromData);
      console.log('toData:', toData);
      console.log('obj:', obj);
    },
    // 监听穿梭框组件移除
    remove(fromData, toData, obj) {
      // 树形穿梭框模式transfer时，返回参数为左侧树移动后数据、右侧树移动后数据、移动的{keys,nodes,halfKeys,halfNodes}对象
      // 通讯录模式addressList时，返回参数为右侧收件人列表、右侧抄送人列表、右侧密送人列表
      console.log('fromData:', fromData);
      console.log('toData:', toData);
      console.log('obj:', obj);
    },
    handlerTree(data, selData) {
      for (let i = data.length - 1; i >= 0; i--) {
        for (let j = selData.length - 1; j >= 0; j--) {
          if (data[i] && data[i].id === selData[j].id) {
            // 当id相等可以删除的情况 即：没有子级可以删除；
            if (!data[i].children && !selData[j].children) {
              data.splice(i, 1);
            } else {
              this.handlerTree(data[i].children, selData[j].children);
            }
          }
        }
      }
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
