<template>
  <el-container class="page-content-wrap table-content">
    <el-card class="width-100 margin-0-auto">
      <el-form :inline="true" class="demo-form-inline">
        <el-form-item>
          <el-input v-model="queryForm.userId" placeholder="玩家Id" clearable />
        </el-form-item>
        <el-form-item>
          <el-select placeholder="请选择注册方式" v-model="queryForm.registeredMode">
              <el-option
              v-for="item in registeredStyle"
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
        <el-button type="primary" icon="el-icon-search" plain>查询</el-button>
        <el-button type="success" icon="el-icon-printer" plain>导出</el-button>
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