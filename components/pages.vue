<template>
  <div class="pages">
    <div class="flex-box block">
      <el-pagination style="display:inline-block;" background @size-change="pageSizeChange" @current-change="pageCurrentChange" :current-page.sync="pageNum" prev-text="　< 上一页　" next-text="　下一页 >　" :page-size="pageSize" layout="prev, pager, next" :total="count">
      </el-pagination>
      <p style="display:inline-block;line-height:28px;" v-if="count==0">第1页 / 共1页</p>
      <p style="display:inline-block;line-height:28px;" v-else>第{{pageNum}}页/共{{Math.ceil(count/pageSize)}}页</p>
      <div style="display:inline-block;margin-left:16px;">到第
        <el-input v-model="input" size="mini" style="width:46px;"></el-input>页</div>
      <div style="display:inline-block;line-height:28px;margin:0 16px;">
        <el-button type="primary" size="mini" @click="pageCurrentNumChange">确定</el-button>
      </div>
    </div>
    <div class="clear"></div>
  </div>

</template>
<script>
export default {
  // count 总页数 pageNum 当前页码 每页条数 pageSize
  props: ['count', 'pageSize'],
  data() {
    return {
      input: 1,
      pageNum: 1
    };
  },
  mounted() { },
  methods: {
    pageSizeChange(val) {
      this.$emit('pageSizeChange', val);
    },
    pageCurrentNumChange() {
      if (this.input) {
        this.pageNum = this.input;
        this.$emit('pageCurrentChange', Number(this.pageNum));
        if (this.input > Math.ceil(this.count / this.pageSize)) {
          if (this.count === 0) {
            this.input = 1;
          } else {
            this.input = Math.ceil(this.count / this.pageSize);
          }
          this.$emit('pageCurrentChange', Number(this.input));
        }
      }
    },
    pageCurrentChange(val) {
      this.pageNum = Number(val);
      this.$emit('pageCurrentChange', Number(this.pageNum));
    }
  },
  watch: {
    // 'pageNum'(val) {
    //   this.pageNum = Number(val);
    //   this.$emit('pageCurrentChange', Number(this.pageNum));
    // }
  }
};
</script>
<style scoped lang="scss">
.pages {
  margin: 30px 0;
}
.clear{
clear: both;
}
.block {
  text-align: right;
  min-width: 400px;
  float:right;

  .red {
    color: red;
  }
}
</style>
