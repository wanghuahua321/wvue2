<template>
  <div class="treess">
    <div v-for="(items, index) in fromData" :key="index" @click.stop="openShow(items)">
      <el-checkbox v-if="items.isLeave" :label="items.label" v-model="items.isCheck" @change.self="changes">{{
        items.label
      }}</el-checkbox>
      <!-- </div> -->
      <div class="floder" v-else>
        <i style="color: #bfbfbf" :class="items.show ? 'el-icon-caret-top' : ' el-icon-caret-bottom'"></i>
        {{ items.label }}
        <b class="allselect" @click.stop="selectalls(items)">全选</b>
      </div>
      <div :class="items.show ? 'shows' : 'hiddens'">
        <Wtrees @changeChcecks="changeChcecks" :fromData="items.children"></Wtrees>
      </div>
    </div>
  </div>
</template>

<script>
import Bus from './bus.js';
export default {
  name: 'Wtrees',
  props: {
    fromData: {
      type: Array,
      default: () => {
        return [];
      }
    },
    allChecks: {
      type: Array,
      default: () => {
        return [];
      }
    }
  },
  data() {
    return {
      checkedCities: [],
      checkAll: [],
      randoms: '',
      numsData: []
    };
  },
  methods: {
    openShow(items) {
      console.log('items', items);
      items.show = !items.show;
    },
    changes() {
      this.randoms = Math.random();
    },
    selectalls(items) {
      console.log('9999e', items);

      this.checkedCities = [];
      this.trueNum = 0;
      this.falseNum = 0;
      this.len = 0;
      this.itearfunc(items);

      console.log('99falseNum9', this.falseNum);
      console.log('9trueNum99', this.trueNum);
      console.log('999', this.len);

      if (this.falseNum == this.len || this.trueNum == this.len) {
        this.itearValue(items, 'all');
      } else if (this.falseNum > 0 || this.trueNum > 0) {
        // this.itearfunc(items);
        this.itearValue(items, 'notall');
      }
    },

    itearfunc(items) {
      let datas = items.children;
      for (let i = 0; i < datas.length; i++) {
        if (datas[i].children && datas[i].children.length) {
          this.itear(datas[i].children);
        } else {
          this.len++;
          if (datas[i].isCheck) {
            this.trueNum++;
          } else if (!datas[i].isCheck) {
            this.falseNum++;
          }
        }
      }
    },

    itearValue(vals, flag) {
      let leaves;
      vals.children ? (leaves = vals.children) : (leaves = vals);
      for (let i = 0; i < leaves.length; i++) {
        if (leaves[i].children && leaves[i].isLeave && !leaves[i].children.length) {
          //最后一个叶子
          if (flag == 'all') {
            leaves[i].isCheck = !leaves[i].isCheck;
          } else {
            leaves[i].isCheck = true;
            console.log('fals', leaves);
          }
        } else {
          this.itearValue(leaves[i].children, flag);
        }
      }
    },
    itear(leaves) {
      for (let i = 0; i < leaves.length; i++) {
        if (leaves[i].children && leaves[i].isLeave) {
          //最后一个叶子
          this.len++;
          if (leaves[i].isCheck) {
            this.trueNum++;
          } else if (!leaves[i].isCheck) {
            this.falseNum++;
          }
        } else {
          this.itear(leaves[i].children);
        }
      }
    },
    allChecksfun(val) {
      let leaves = val.children ? val.children : val;
      // console.log('this.allChecks.length', this.allChecks.length);
      for (let i = 0; i < leaves.length; i++) {
        if (leaves[i].children && leaves[i].isLeave) {
          //最后一个叶子
          for (let j = 0; j < this.allChecks.length; j++) {
            console.log('this.allChecks[j]', this.allChecks[j].id);
            console.log('leaves[i].id', leaves[i].id);

            if (this.allChecks[j].id == leaves[i].id) {
              // this.numsData.push(leaves[i].id);
              console.log('00000000', leaves[i].id);
              leaves[i].isCheck = !this.allChecks[j].isCheck;
              break;
            }
          }
        } else {
          this.allChecksfun(leaves[i].children);
        }
      }
    },

    changeChcecks() {}
  },
  watch: {
    randoms() {
      // console.log('newsData', newsData);
      Bus.$emit('changeChcecks', this.fromData);

      console.log('00000', this.fromData);
    },
    allChecks() {
      this.numsData = [];
      // this.allChecksfun(this.fromData[0]);
      // console.log('--------', this.numsData);
      // console.log('909', this.fromData);
      // console.log('lastdata', this.allChecksfun(this.fromData[0]));
      // this.allChecksfuns(this.fromData[0]);
    }
  }
};
</script>

<style>
.treess {
  padding-left: 10px;
}
.floder {
  position: relative;
  width: 200px;
}

.allselect {
  position: absolute;
  right: 20px;
  color: #595959;
  font-size: 14px;
  font-weight: normal;
}
.yezi {
  color: red;
}

.shows {
  display: block;
}
.hiddens {
  display: none;
}
</style>
