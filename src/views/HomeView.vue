<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <!-- <Wtrees :fromData="fromData"></Wtrees> -->
    <transfers></transfers>

    <el-table
      ref="multipleTable"
      :data="tableData"
      tooltip-effect="dark"
      style="width: 100%"
      @selection-change="handleSelectionChange"
    >
      <el-table-column type="selection" width="55"> </el-table-column>
      <el-table-column label="日期" width="120">
        <template slot-scope="scope">{{ scope.row.date }}</template>
      </el-table-column>
      <el-table-column prop="name" label="姓名" width="120"> </el-table-column>
      <el-table-column prop="address" label="地址" show-overflow-tooltip> </el-table-column>
    </el-table>
    <div style="margin-top: 20px">
      <el-button @click="toggleSelection([tableData[1], tableData[2]])">切换第二、第三行的选中状态</el-button>
      <el-button @click="toggleSelection()">取消选择</el-button>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue';
// import Wtrees from '@/components/Wtrees.vue';
import transfers from '@/components/transfers.vue';

export default {
  name: 'HomeView',
  components: {
    HelloWorld,

    transfers
  },
  data() {
    return {
      fromData: [
        {
          id: '1',
          pid: 0,
          label: '一级 1',
          show: true,
          children: [
            {
              id: '1-1',
              pid: '1',
              label: '二级 1-1',
              show: true,
              children: [
                {
                  id: '1-2s-1',
                  pid: '1-3',
                  children: [],
                  label: 'san级 1-2s-1',
                  isLeave: true,
                  isCheck: false
                },
                {
                  id: '1-2ds-2',
                  pid: '1-3',
                  children: [],
                  label: 'san级 1-2s-2',
                  isLeave: true,
                  isCheck: false
                }
              ]
            },
            {
              id: '1-2',
              pid: '2',
              label: '二级 1-21',
              show: true,
              children: [
                {
                  id: '1-2s-21',
                  pid: '1-23',
                  children: [],
                  label: 'san级 1-22s-1',
                  isLeave: true,
                  isCheck: false
                },
                {
                  id: '1-2d2s-2',
                  pid: '1-23',
                  children: [],
                  label: 'san级 1-22s-2',
                  isLeave: true,
                  isCheck: false
                }
              ]
            }
          ]
        }
      ],
      tableData: [
        {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-08',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-06',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-07',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }
      ],
      multipleSelection: []
    };
  },
  methods: {
    toggleSelection(rows) {
      console.log('rows', rows);
      if (rows) {
        rows.forEach((row) => {
          this.$refs.multipleTable.toggleRowSelection(row);
        });
      } else {
        this.$refs.multipleTable.clearSelection();
      }
    },
    handleSelectionChange(val) {
      this.multipleSelection = val;
    }
  }
};
</script>
