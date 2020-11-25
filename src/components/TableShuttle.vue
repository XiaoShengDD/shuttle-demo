<template>
  <div class="table-shuttle">
    <el-table
      ref="multipleTable1"
      :data="tableData1"
      tooltip-effect="dark"
      style="width: 100%"
      @selection-change="handleSelectionChange1"
    >
      <el-table-column type="selection" width="55"></el-table-column>
      <el-table-column label="日期" width="120">
        <template slot-scope="scope">{{ scope.row.date }}</template>
      </el-table-column>
      <el-table-column prop="name" label="姓名" width="120"></el-table-column>
      <el-table-column prop="address" label="地址" show-overflow-tooltip></el-table-column>
    </el-table>

    <el-table
      ref="multipleTable2"
      :data="tableData2"
      tooltip-effect="dark"
      style="width: 100%"
      @select="handleSelectionChange2"
      @select-all="handleSelectionChange2"
    >
      <el-table-column type="selection" width="55"></el-table-column>
      <el-table-column label="日期" width="120">
        <template slot-scope="scope">{{ scope.row.date }}</template>
      </el-table-column>
      <el-table-column prop="name" label="姓名" width="120"></el-table-column>
      <el-table-column prop="address" label="地址" show-overflow-tooltip></el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  name: 'Tshuttle',
  data() {
    return {
      tableData2: [],
      tableData1: [
        {
          id: 1,
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄',
        },
        {
          id: 2,
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄',
        },
        {
          id: 3,
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄',
        },
        {
          id: 4,

          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄',
        },
        {
          id: 5,

          date: '2016-05-08',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄',
        },
        {
          id: 6,

          date: '2016-05-06',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄',
        },
        {
          id: 7,

          date: '2016-05-07',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄',
        },
      ],
    }
  },
  watch: {
    tableData2: function (newVal, oldVal) {
      let newArray = oldVal.filter((item) => {
        let arraids = []
        newVal.forEach((item, i) => {
          arraids.push(item.id)
        })
        return arraids.indexOf(item.id) == -1
      })
      newArray.forEach((val, index) => {
        this.$refs.multipleTable1.toggleRowSelection(val, false)
      })
      this.$nextTick(() => {
        this.getDefault()
      })
    },
  },

  methods: {
    handleSelectionChange1(row) {
      this.tableData2 = row
    },
    handleSelectionChange2(selection, row) {
      if (row) {
        this.tableData2 = this.tableData2.filter((item) => item.id != row.id)
      } else {
        this.tableData2 = []
      }
    },
    getDefault() {
      this.tableData2.forEach((val, index) => {
        this.$refs.multipleTable2.toggleRowSelection(val, true)
      })
    },
  },
}
</script>

<style>
</style>
