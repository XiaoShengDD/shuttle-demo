<template>
  <div class="shuttle">
    <div class="box">
      <div class="left">
        <el-tree
          :props="props"
          :load="loadNode"
          node-key="id"
          lazy
          show-checkbox
          @check-change="handleCheckChange"
          ref="tree"
        ></el-tree>
      </div>
      <div class="right">
        <ul>
          <li v-for="item in nodeList" :key="item.id">
            <p>{{ item.name }}</p>
          </li>
        </ul>
      </div>
    </div>
    <el-button @click="submit" size="small" type="primary">主要按钮</el-button>
  </div>
</template>

<script>
export default {
  name: 'Shuttle',
  data() {
    return {
      props: {
        label: 'name',
        children: 'zones',
      },
      count: 1,
      nodeList: [],
    }
  },
  methods: {
    handleCheckChange() {
      let idList = []
      idList = [
        ...this.$refs.tree.getCheckedKeys(),
        ...this.$refs.tree.getHalfCheckedKeys(),
      ]
      if (idList.length == 0) {
        return false
      }
      var a = []
      idList.forEach((item) => {
        let b = this.$refs.tree.getNode(item)
        a.push({
          id: b.id,
          name: b.label,
        })
      })
      this.nodeList = a
    },

    loadNode(node, resolve) {
      if (node.level === 0) {
        return resolve([
          { name: 'region' + Math.random() * 10000, id: Math.random() * 10000 },
          {
            name: 'region' + Math.random() * 10000,
            id: Math.random() * 10000,
          },
        ])
      }

      setTimeout(() => {
        var data

        data = [
          {
            id: Math.random() * 10000,
            name: 'zone' + Math.random() * 10000,
          },
          {
            id: Math.random() * 10000,
            name: 'zone' + Math.random() * 10000,
          },
        ]

        resolve(data)
        this.handleCheckChange()
      }, 500)
    },

    submit() {
      alert(JSON.stringify(this.nodeList))
    },
  },
}
</script>

<style>
.box {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 500px;
}

.left,
.right {
  height: 500px;
  width: 240px;
  border: 1px solid #ccc;
}
</style>
