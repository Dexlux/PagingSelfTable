# PagingSelfTable
主要用于有一堆数据需要前端自行分页-二次封装element Table组件

# Example
```javascript
<template>
  <div class="app-container">
    <PagingSelfTable :all-data="allData" stripe>
      <el-table-column label="序号" type="index" width="50" />
      <el-table-column prop="date" label="日期" width="180" />
      <el-table-column prop="name" label="姓名" width="180" />
      <el-table-column prop="address" label="地址" />
      <el-table-column fixed="right" label="操作" width="120">
        <template slot-scope="scope">
          <el-button type="text" size="small" @click.native.prevent="deleteRow(scope.$index)">
            移除
          </el-button>
        </template>
      </el-table-column>
    </PagingSelfTable>
  </div>
</template>

<script>
import PagingSelfTable from './PagingSelfTable.vue'

export default {
  name: 'Example',
  components: {
    PagingSelfTable
  },
  data() {
    return {
      allData: [
        {
          date: '2016-05-02',
          name: '王小虎1',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-04',
          name: '王小虎2',
          address: '上海市普陀区金沙江路 1517 弄'
        },
        {
          date: '2016-05-01',
          name: '王小虎3',
          address: '上海市普陀区金沙江路 1519 弄'
        },
        {
          date: '2016-05-03',
          name: '王小虎4',
          address: '上海市普陀区金沙江路 1516 弄'
        },
        {
          date: '2016-05-02',
          name: '王小虎5',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-04',
          name: '王小虎6',
          address: '上海市普陀区金沙江路 1517 弄'
        },
        {
          date: '2016-05-01',
          name: '王小虎7',
          address: '上海市普陀区金沙江路 1519 弄'
        }
      ]
    }
  },
  methods: {
    deleteRow(index) {
      this.allData.splice(index, 1)
      console.log(index, this.allData)
    }
  }
}
</script>
```
