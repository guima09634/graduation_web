<template>
  <el-container class="page-content-wrap table-content">
    <el-card class="width-100 margin-0-auto">
      <el-form :inline="true" class="demo-form-inline">
        <el-form-item>
          <el-input v-model="queryForm.gameName" placeholder="请输入游戏的名字" clearable />
        </el-form-item>
        <el-form-item>
          <el-select placeholder="请选择配置类型" v-model="queryForm.type">
              <el-option
              v-for="item in structureType"
              :key="item.index"
              :value="item.value"
              :label="item.label"
              >
              </el-option>
          </el-select>
        </el-form-item>
        <el-form-item>
            <el-date-picker
                v-model="queryForm.startTime"
                type="datetime"
                placeholder="选择开始时间"
                align="right"
                :picker-options="pickerOptions">
            </el-date-picker>
        </el-form-item>
        <el-form-item>
          <el-date-picker
                v-model="queryForm.endTime"
                type="datetime"
                placeholder="选择结束时间"
                align="right"
                :picker-options="pickerOptions">
            </el-date-picker>
        </el-form-item>
      </el-form>
      <div class="button-list">
        <el-button type="primary" icon="el-icon-search" @click="query" round plain>查询</el-button>
        <el-button type="success" icon="el-icon-plus" round plain>添加</el-button>
        <el-button type="warning" icon="el-icon-edit" round plain>修改</el-button>
        <el-button type="danger" icon="el-icon-delete" round plain>删除</el-button>
      </div>
      <el-table
            ref="multipleTable"
            :data="tableData"
            v-loading="tableLoading" class="width-100"
            @select-all="handleSelectionChange" @select="handleSelectionChange">
            <el-table-column
            type="selection"
            width="55">
            </el-table-column>
            <el-table-column
            prop="userId"
            label="玩家账号"
            width="120">
            <template slot-scope="scope">{{ scope.row.userId }}</template>
            </el-table-column>
            <el-table-column
            prop="mode"
            label="玩家注册方式"
            width="120">
            </el-table-column>
            <el-table-column
            prop="dependences"
            label="注册依赖"
            show-overflow-tooltip>
            </el-table-column>
        </el-table>
    </el-card>
  </el-container>
</template>

<script>
export default {
    data (){
        return {
            structureType: [
                {value:'vip', label:'vip特权配置'}, 
                {value:'first', label:'首储配置'}, 
            ],
            pickerOptions: {
                disabledDate(time) {
                    return time.getTime() > Date.now();
                },
                shortcuts: [{
                    text: '今天',
                    onClick(picker) {
                    picker.$emit('pick', new Date());
                    }
                }, {
                    text: '昨天',
                    onClick(picker) {
                    const date = new Date();
                    date.setTime(date.getTime() - 3600 * 1000 * 24);
                    picker.$emit('pick', date);
                    }
                }, {
                    text: '一周前',
                    onClick(picker) {
                    const date = new Date();
                    date.setTime(date.getTime() - 3600 * 1000 * 24 * 7);
                    picker.$emit('pick', date);
                    }
                }]
            },
            queryForm: {
                gameName:'',
                type:'',
                startTime:'',
                endTime:''
            },
            tableLoading: false,
            selectData:[],
            tableData:[]
        }
    },
    methods: {
        handleSelectionChange (val) {
            this.selectData = val
        },

        query() {
          this.$axios({
              url:'http://localhost:9090/api/user/query',
              method:'post',
              data:this.queryForm
          }).then( (res) => {
              console.log(res.data);
          },error => {
              console.log(error)
          }).catch(error => {
              console.log(error);
          })
        }
    }
}
</script>
