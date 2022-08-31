<template>
  <div class="transfers">
    <div class="t_left">
      <div class="left_tit">报表列表</div>
      <Wtrees ref="trees" :fromData="fromData" @changeChceck="changeChcecks" :allChecks="allCheckscope"></Wtrees>
    </div>
    <div class="t_cent">
      <div class="transBtn">
        <div @click="toRight" :class="fromData.length ? '_leftActive _left' : '_left'">></div>
        <div @click="toLeft" :class="checkedCities.length ? '_leftActive _rig' : '_rig'">d</div>
      </div>
    </div>
    <div class="t_rig">
      <div class="left_tit">已选报表</div>
      <div class="check_alls">
        <div class="check_item"></div>

        <el-checkbox-group v-if="allChecks.length" v-model="checkedCities">
          <el-checkbox class="grounp" v-for="i in allChecks" :key="i.id" :label="i.id">
            <span class="kindsReport">QIikView</span> <b>{{ i.label }}</b>
          </el-checkbox>
        </el-checkbox-group>

        <div v-else>暂无数据</div>
      </div>
    </div>
  </div>
</template>

<script>
import Wtrees from './Wtrees';
import Bus from './bus.js';
export default {
  name: 'transfers',
  components: {
    Wtrees
  },
  props: {
    // fromData: [],
    // default: () => {
    //   return [];
    // }
  },
  data() {
    return {
      checkedCities: ['1-2s9-21'],
      checkedCities1: ['1-2s-1', '1-2-2'],
      checkAll: [],
      allFormdata: [],
      allChecks: [],
      allCheckscope: [],
      trueNum: 0,
      falseNum: 0,
      len: 0,
      // fromDatas: [],
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
                  label: 'san级1-2s-1',
                  isLeave: true,
                  isCheck: false
                },
                {
                  id: '1-2-2',
                  pid: '1-3',
                  children: [],
                  label: 'san级j1-2s-2',
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
                  id: '1-2s9-21',
                  pid: '1-23',
                  children: [],
                  label: 'san级001-22s-1',
                  isLeave: true,
                  isCheck: false
                },
                {
                  id: '1-276s-2',
                  pid: '1-23',
                  children: [],
                  label: 'san级 =hhh1-22s-2',
                  isLeave: true,
                  isCheck: false
                }
              ]
            }
          ]
        }
      ],
      datas: [
        {
          id: '2',
          reportId: 0,
          label: 'Everyone',
          imgUrl: null,
          biProductId: 0,
          reportType: null,
          isReport: false,
          type: 1,
          _GroupImage: '',
          groupImage: '',
          groupIcon: '',
          children: [
            {
              id: '3',
              reportId: 0,
              label: '1',
              imgUrl: null,
              biProductId: 0,
              reportType: null,
              isReport: false,
              type: 1,
              _GroupImage: null,
              groupImage: null,
              groupIcon: null,
              children: [
                {
                  id: '3-1',
                  reportId: 1,
                  label: '我的新工作表',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                }
              ]
            },
            {
              id: '4',
              reportId: 0,
              label: 'My App',
              imgUrl: null,
              biProductId: 0,
              reportType: null,
              isReport: false,
              type: 1,
              _GroupImage: null,
              groupImage: null,
              groupIcon: null,
              children: [
                {
                  id: '4-2',
                  reportId: 2,
                  label: '我的新工作表',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                }
              ]
            },
            {
              id: '5',
              reportId: 0,
              label: '测试',
              imgUrl: null,
              biProductId: 0,
              reportType: null,
              isReport: false,
              type: 1,
              _GroupImage: null,
              groupImage: null,
              groupIcon: null,
              children: [
                {
                  id: '5-3',
                  reportId: 3,
                  label: '我的新工作表',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                }
              ]
            },
            {
              id: '6',
              reportId: 0,
              label: '测试api',
              imgUrl: null,
              biProductId: 0,
              reportType: null,
              isReport: false,
              type: 1,
              _GroupImage: null,
              groupImage: null,
              groupIcon: null,
              children: [
                {
                  id: '6-4',
                  reportId: 4,
                  label: '我的新工作表',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                }
              ]
            },
            {
              id: '7',
              reportId: 0,
              label: '超市演示数据',
              imgUrl: null,
              biProductId: 0,
              reportType: null,
              isReport: false,
              type: 1,
              _GroupImage: null,
              groupImage: null,
              groupIcon: null,
              children: [
                {
                  id: '7-5',
                  reportId: 5,
                  label: '_Kpi',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '7-9',
                  reportId: 9,
                  label: '产品分析',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '7-8',
                  reportId: 8,
                  label: '明细表',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '7-10',
                  reportId: 10,
                  label: '我的新工作表',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '7-6',
                  reportId: 6,
                  label: '销售和利润分析',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '7-11',
                  reportId: 11,
                  label: '销售和利润分析 (1)',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '7-7',
                  reportId: 7,
                  label: '仪表盘概览',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                }
              ]
            }
          ]
        },
        {
          id: '8',
          reportId: 0,
          label: 'Monitoring apps',
          imgUrl: null,
          biProductId: 0,
          reportType: null,
          isReport: false,
          type: 1,
          _GroupImage: '',
          groupImage: '',
          groupIcon: '',
          children: [
            {
              id: '9',
              reportId: 0,
              label: 'License Monitor',
              imgUrl: null,
              biProductId: 0,
              reportType: null,
              isReport: false,
              type: 1,
              _GroupImage: null,
              groupImage: null,
              groupIcon: null,
              children: [
                {
                  id: '9-12',
                  reportId: 12,
                  label: 'Allocation History',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '9-17',
                  reportId: 17,
                  label: 'Log Details',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '9-18',
                  reportId: 18,
                  label: 'Login Access History',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '9-16',
                  reportId: 16,
                  label: 'Overview',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '9-15',
                  reportId: 15,
                  label: 'Timeline',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '9-14',
                  reportId: 14,
                  label: 'Unified Licensing History',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '9-13',
                  reportId: 13,
                  label: 'Usage by App',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '9-20',
                  reportId: 20,
                  label: 'Usage Snapshot',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '9-19',
                  reportId: 19,
                  label: 'User Access History',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '9-21',
                  reportId: 21,
                  label: 'User Detail',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                }
              ]
            },
            {
              id: '10',
              reportId: 0,
              label: 'Operations Monitor',
              imgUrl: null,
              biProductId: 0,
              reportType: null,
              isReport: false,
              type: 1,
              _GroupImage: null,
              groupImage: null,
              groupIcon: null,
              children: [
                {
                  id: '10-34',
                  reportId: 34,
                  label: '24-Hour Summary',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '10-24',
                  reportId: 24,
                  label: 'Apps',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '10-28',
                  reportId: 28,
                  label: 'Export Links for Cloud',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '10-27',
                  reportId: 27,
                  label: 'Export Overview',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '10-23',
                  reportId: 23,
                  label: 'Log Details',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '10-25',
                  reportId: 25,
                  label: 'Performance',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '10-26',
                  reportId: 26,
                  label: 'QMC Change Log',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '10-31',
                  reportId: 31,
                  label: 'Session Details',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '10-22',
                  reportId: 22,
                  label: 'Session Overview',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '10-29',
                  reportId: 29,
                  label: 'Sheet Usage',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '10-33',
                  reportId: 33,
                  label: 'Task Details',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '10-30',
                  reportId: 30,
                  label: 'Task Overview',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                },
                {
                  id: '10-32',
                  reportId: 32,
                  label: 'Task Planning',
                  imgUrl: null,
                  biProductId: 1,
                  reportType: 'GranDataBI',
                  isReport: true,
                  type: 1,
                  _GroupImage: null,
                  groupImage: null,
                  groupIcon: null,
                  children: []
                }
              ]
            }
          ]
        }
      ],
      allleave: [],
      isflag: 'mountd'
    };
  },
  methods: {
    dealtreeData(treeData) {
      treeData.map((res) => {
        if (!res.children.length) {
          res.isCheck = false;
          res.isLeave = true;
        } else {
          res.show = true;
          this.dealtreeData(res.children);
        }
      });
      this.fromDatas = treeData;
    },
    changeChcecks() {
      this.checkedCities = [];
      console.log('9s9', this.$refs.trees.fromData);
      this.allFormdata = this.$refs.trees.fromData;
      this.allChecks = [];
      for (let i = 0; i < this.allFormdata.length; i++) {
        if (this.allFormdata[i].children) {
          this.isflag = 'toright';
          this.itear(this.allFormdata[i].children);
        }
      }
    },
    itear(leaves) {
      console.log('0-', leaves);
      for (let i = 0; i < leaves.length; i++) {
        if (leaves[i].children && leaves[i].isLeave) {
          //最后一个叶子
          if (this.isflag == 'mountd') {
            if (this.checkedCities.length) {
              this.checkedCities.map((res) => {
                if (res == leaves[i].id) {
                  leaves[i].isCheck = true;
                  console.log(')000000888');
                  this.allChecks.push(leaves[i]);
                }
              });
            }
          } else if (this.isflag == 'toright') {
            if (leaves[i].isCheck) {
              this.allChecks.push(leaves[i]);
            }
          } else {
            this.checkedCities.map((res) => {
              if (res == leaves[i].id) {
                leaves[i].isCheck = false;
              }
            });
          }
        } else {
          this.itear(leaves[i].children);
        }
      }
      this.allleave = leaves;
    },
    toRight() {
      this.changeChcecks();
    },
    toLeft() {
      if (this.checkedCities.length) {
        for (let i = 0; i < this.checkedCities.length; i++) {
          for (let j = 0; j < this.allChecks.length; j++) {
            if (this.checkedCities[i] == this.allChecks[j].id) {
              this.allCheckscope.push(this.allChecks[j]);
              this.allChecks.splice(j, 1);
            }
          }
        }
      }
      this.isflag = 'toLeft';
      this.itear(this.fromData[0].children);
    }
  },
  mounted() {
    Bus.$on('changeChcecks', () => {});
    // this.itear(this.fromData[0].children);
  },
  created() {
    this.dealtreeData(this.datas);
  }
};
</script>

<style scoped>
.kindsReport {
  margin: 5px 10px;
  background: #d9e5ff;
  padding: 2px 6px;
  font-size: 12px;
  color: #2797ff;
}
.qlikSence {
  background: #e6f7ff;
  color: #4881ff;
}
.transfers {
  display: flex;
  width: 600px;
  height: 300px;
}
.t_left {
  width: 40%;

  border: 1px solid #d8d8d8;
}
.treess {
  overflow: auto;
  height: calc(100% - 34px);
}
.t_cent {
  width: 20%;
}
.t_rig {
  width: 40%;
  border: 1px solid #d8d8d8;
}
.left_tit {
  border-bottom: 1px solid #d8d8d8;
  padding: 6px 12px;
}

.transBtn {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.transBtn ._left {
  border-radius: 6px;
  background: #ffffff;
  color: #d9d9d9;
  border: 2px solid #d9d9d9;
  min-width: 36px;
  min-height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
}
._leftActive {
  background: #1890ff !important;
  color: #fff !important;
  border-color: #1890ff !important;
}

.transBtn ._rig {
  border-radius: 6px;
  background: #ffffff;
  color: #d9d9d9;
  border: 2px solid #d9d9d9;
  min-width: 36px;
  min-height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 20px;
}

.grounp {
  display: flex !important;
  margin: 10px 7px !important;
}

:deep(.el-checkbox__label) {
  padding-left: 8px !important;
  color: #363636;
}
</style>
