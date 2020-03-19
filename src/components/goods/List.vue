<template>
  <div>
    <!-- 面包屑导航区 -->
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item>商品管理</el-breadcrumb-item>
        <el-breadcrumb-item>商品列表</el-breadcrumb-item>
      </el-breadcrumb>
      <el-card>
        <el-row :gutter="20">
          <el-col :span="8">
            <el-input placeholder="请输入内容" v-model="queryInfo.query" clearable @clear="getGoodsList">
              <el-button slot="append" icon="el-icon-search" @click="getGoodsList"></el-button>
            </el-input>
          </el-col>
          <el-col :span="4">
              <el-button type="primary" @click="goAddPage">添加商品</el-button>
          </el-col>
        </el-row>
        <el-table :data="goodsList" stripe border>
          <el-table-column type="index" label="#">
          </el-table-column>
          <el-table-column  label="商品名称" prop="goods_name">
          </el-table-column>
          <el-table-column  label="商品价格(元)" prop="goods_price" width="95px">
          </el-table-column>
          <el-table-column  label="商品重量" prop="goods_weight" width="70px">
          </el-table-column>
          <el-table-column  label="创建日期" prop="add_time" width="140px">
            <template slot-scope="scope">
              {{scope.row.add_time | dateFormat}}
            </template>
          </el-table-column>
          <el-table-column  label="操作" width="130px">
            <template slot-scope="">
              <el-button type="primary" icon="el-icon-edit" size="mini"></el-button>
              <el-button type="danger" icon="el-icon-delete" size="mini"></el-button>
            </template>
          </el-table-column>
        </el-table>
        <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page="queryInfo.pagenum"
          :page-sizes="[5, 10, 15, 20]"
          :page-size="queryInfo.pageSize"
          layout="total, sizes, prev, pager, next, jumper"
          :total="total" background>
        </el-pagination>
      </el-card>
  </div>
</template>
<script>
export default {
  data () {
    return {
      // 查询参数
      queryInfo: {
        query: '',
        pagenum: 1,
        pagesize: 10
      },
      // 商品列表
      goodsList: [],
      // 总数据数
      total: 0
    }
  },
  created () {
    this.getGoodsList()
  },
  methods: {
    // 根据分页获取对应的商品列表
    async getGoodsList () {
      const { data: res } = await this.$http.get('goods', { params: this.queryInfo })
      if (res.meta.status !== 200) return this.$message.error('获取商品列表失败！')
      this.$message.success('获取商品列表成功')
      console.log(res.data)
      this.goodsList = res.data.goods
      this.total = res.data.total
    },
    // 拿到最新的 pageSize
    handleSizeChange (newSize) {
      this.queryInfo.pagesize = newSize
      this.getGoodsList()
    },
    // 当前页码值发生变化
    handleCurrentChange (newPage) {
      this.queryInfo.pagenum = newPage
      this.getGoodsList()
    },
    goAddPage () {
      this.$router.push('/goods/add')
    }
  }
}
</script>
<style lang="less" scoped>

</style>
