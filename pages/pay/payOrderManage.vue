<template>
  <el-container class="page-content-wrap table-content">
    <el-card class="width-100 margin-0-auto">
      <el-form :inline="true" class="demo-form-inline">
        <el-form-item>
          <el-input v-model="queryForm.userId" placeholder="请输入玩家Id" size="mini" clearable />
        </el-form-item>
        <el-form-item>
          <el-input v-model="queryForm.creditId" placeholder="请输入订单号" size="mini" clearable />
        </el-form-item>
         <el-form-item>
          <el-input v-model="queryForm.gameName" placeholder="请输入游戏名字" size="mini" clearable />
        </el-form-item>
        <el-form-item>
          <el-select placeholder="请选择第三方支付平台" size="mini" v-model="queryForm.platform">
              <el-option
              v-for="item in payPlatform"
              :key="item.index"
              :value="item.value"
              :label="item.label"
              >
              </el-option>
          </el-select>
        </el-form-item>
        <el-form-item>
          <el-input-number placeholder="请输入起始金额" v-model="queryForm.startAmount" size="mini" :precision="0.1" :step="0.1" :max="500000"></el-input-number>
        </el-form-item>
        <el-form-item>
          <el-input-number placeholder="请输入结束金额" v-model="queryForm.endAmount" size="mini" :precision="0" :step="0.1" :max="500000"></el-input-number>
        </el-form-item>
        <!--<el-form-item>
            <el-date-picker
                v-model="queryForm.startTime"
                type="datetime"
                placeholder="选择开始时间"
                align="right"
                size="mini"
                :picker-options="pickerOptions">
            </el-date-picker>
        </el-form-item>
        <el-form-item>
          <el-date-picker
                v-model="queryForm.endTime"
                type="datetime"
                placeholder="选择结束时间"
                align="right"
                size="mini"
                :picker-options="pickerOptions">
            </el-date-picker>
        </el-form-item>-->
      </el-form>
      <div class="button-list">
        <el-button type="primary" icon="el-icon-search" @click="query" plain>查询</el-button>
        <el-button type="success" icon="el-icon-printer" plain>导出</el-button>
        <el-button type="danger" icon="el-icon-printer" plain>补发</el-button>
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
            payPlatform: [
                {value:'alipay', label:'支付宝'}, 
                {value:'weixin', label:'微信支付'}, 
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
                userId:'',
                creditId:'',
                platform:'',
                startAmout:'',
                endAmount:'',
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
