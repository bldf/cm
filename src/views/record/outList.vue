<template>
  <div>
    <el-card shadow="never" :body-style="{ padding: '0px' }">
      <div slot="header">
        <el-form :inline="true" :model="searchInfo" class="demo-form-inline">
          <el-form-item label="用户名">
            <el-input v-model="searchInfo.user" placeholder="用户名"></el-input>
          </el-form-item>
          <el-form-item label="出门日期">
            <el-date-picker type="daterange" v-model="dateRange" align="right" unlink-panels range-separator="至" start-placeholder="出门开始日期" end-placeholder="出门结束日期" :picker-options="$store.state.dateRangePickerOptions">
            </el-date-picker>
          </el-form-item>
          <el-form-item>
            <el-button type="info">重置</el-button>
            <el-button type="primary" icon="el-icon-search">查询</el-button>
          </el-form-item>
        </el-form>
      </div>

      <el-table :data="pager.records" style="width: 100%"  highlight-current-row v-loading="$store.state.loading" @selection-change="onSelectionChange">

        <el-table-column type="expand">
          <template slot-scope="props">
            <el-form label-position="left" inline class="demo-table-expand">
              <el-form-item  width="140" label="物品详情1">
                <span>001零件号1箱</span>
              </el-form-item>
              <el-form-item  width="140" label="物品详情2">
                <span>007零件号1箱</span>
              </el-form-item>
              <el-form-item   width="140" label="物品详情3">
                <span>006零件号1箱</span>
              </el-form-item>
              <el-form-item  width="140" label="物品详情4">
                <span>005零件号1箱</span>
              </el-form-item>
              <el-form-item  width="140" label="物品详情5">
                <span>004零件号1箱</span>
              </el-form-item>
              <el-form-item   width="140" label="物品详情6">
                <span>003零件号1箱</span>
              </el-form-item>
              <el-form-item  width="140" label="物品详情7">
                <span>002零件号1箱</span>
              </el-form-item>
            </el-form>
          </template>
        </el-table-column>


        <el-table-column prop="userName" label="发起账户"></el-table-column>
        <el-table-column prop="userName" label="用户名"></el-table-column>
        <el-table-column label="发起描述" width="150">
          <template slot-scope="scope">
            {{ '+' + scope.row.nation + ' ' + scope.row.phone }}
          </template>
        </el-table-column>

        <el-table-column label="发起日期" width="140">
          <template slot-scope="scope">
            {{ scope.row.createDate | moment('YYYY-MM-DD hh:mm') }}
          </template>
        </el-table-column>
        <el-table-column label="放行日期" width="140">
          <template slot-scope="scope">
            {{ scope.row.signInDate | moment('YYYY-MM-DD hh:mm') }}
          </template>
        </el-table-column>
        <el-table-column label="状态" width="120">
          <template slot-scope="scope">

            <el-tag size="medium">放行通过</el-tag>
            <!--</el-switch>-->
          </template>
        </el-table-column>
      </el-table>
      <!--分页插件-->
      <el-pagination :current-page="pager.current" :page-size="pager.size" :total="pager.total" class="pagination text-right" :page-sizes="$store.state.paginationPageSizes" :layout="$store.state.paginationLayout"></el-pagination>
    </el-card>
  </div>
</template>
<style>
  .input-with-select .el-input-group__prepend {
    background-color: #fff;
  }
  .cell {
    text-align: center;
  }
  .demo-table-expand {
    font-size: 0;
  }
  .demo-table-expand label {
    width: 90px;
    color: #99a9bf;
  }
  .demo-table-expand .el-form-item {
    margin-right: 0;
    margin-bottom: 0;
    width: 33.33333%;
  }
</style>
<script>
    export default {
        name: "inList",
        data() {
            return {
                searchInfo:{},
                diaInfo:{},
                dialogVisible: false,
                state: null,
                dateRange: null,
                test: null,
                test1: null,
                selectedRows: [],
                bucketName: "public",
                pager: { current: 1, size: 10, total: 0, records: [] }
            };
        },
        mounted() {
            this.query();
        },
        methods: {
            searchFn(){
                console.log(this.searchInfo)
            },
            query() {
                this.$http.get("/user").then(res => {
                    this.pager = res.data;
                });
            },
            edit() {
                this.dialogVisible = true;
            },
            onSelectionChange(rows) {
                this.selectedRows = rows.map(item => item.userId);
            },
            remove() {
                this.$confirm(`此操作将永久删除, 是否继续?</br>共用户【${this.selectedRows.length}】个`, "删除确认", {
                    confirmButtonText: "确定",
                    cancelButtonText: "取消",
                    dangerouslyUseHTMLString: true,
                    type: "warning"
                });
            },
            onRemoveFile(file) {
                this.$http.delete(`/oss/remove/${this.bucketName}/${file.response}`);
            }
        }
    };
</script>
