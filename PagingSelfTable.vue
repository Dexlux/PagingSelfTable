<template>
  <div>
    <el-table :data="tableData" border v-bind="$attrs" v-on="$listeners">
      <slot />
    </el-table>
    <el-pagination :current-page="page" :page-size="size" :page-sizes="pageSizes" layout="total, sizes, prev, pager, next, jumper" :total="total" @size-change="sizeChange" @current-change="currentChange" />
  </div>
</template>
<script>
export default {
  props: {
    // 全部数据(待分页)
    allData: {
      required: true,
      type: Array,
      default: () => []
    },
    // 可选择的一页多少条
    pageSizes: {
      type: Array,
      default: () => [10, 50, 100]
    }
  },
  data() {
    return {
      page: 1, // 第几页
      total: 0, // 总条目数
      tableData: [], // 表格绑定的数据
      sizeTemp: null // 一页多少条的缓存数据
    }
  },
  computed: {
    // 一页多少条
    size: {
      get() {
        return this.sizeTemp || this.pageSizes[0]
      },
      set(val) {
        this.sizeTemp = val
      }
    }
  },
  watch: {
    // 数据更新时，重新获取表格数据
    allData: {
      handler() {
        this.getTabelData()
      },
      immediate: true
    }
  },
  methods: {
    // 获取表格数据，自行分页(slice)
    getTabelData() {
      // allData为全部数据
      this.tableData = this.allData.slice(
        (this.page - 1) * this.size,
        this.page * this.size
      )
      this.total = this.allData.length
    },
    // page改变时的回调函数，参数为当前页码
    currentChange(val) {
      console.log('翻页，当前为第几页', val)
      this.page = val
      this.getTabelData()
    },
    // size改变时回调的函数，参数为当前的size
    sizeChange(val) {
      console.log('改变每页多少条，当前一页多少条数据', val)
      this.size = val
      this.page = 1
      this.getTabelData()
    }
  }
}
</script>
