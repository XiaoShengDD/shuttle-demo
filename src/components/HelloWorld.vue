<template>
  <div class="shuttle">
    <div class="box">
      <div class="left">
        <el-tree
          :props="props"
          :load="loadNode"
          lazy
          show-checkbox
          @check-change="handleCheckChange"
        >
        </el-tree>
      </div>
      <div class="right">
        <ul>
          <li v-for="item in nodeList" :key="item.id">
            <p>{{ item.label }}</p>
          </li>
        </ul>
      </div>
    </div>
    <el-button @click="submit" size="small" type="primary">主要按钮</el-button>
  </div>
</template>

<script>
export default {
  name: "Shuttle",
  data() {
    return {
      props: {
        label: "name",
        children: "zones",
      },
      count: 1,
      nodeList: [],
    };
  },
  methods: {
    handleCheckChange(data, checked, indeterminate) {
      console.log(data, checked, indeterminate);
    },

    loadNode(node, resolve) {
      if (node.level === 0) {
        return resolve([{ name: "region1" }, { name: "region2" }]);
      }
      if (node.level > 3) return resolve([]);

      var hasChild;
      if (node.data.name === "region1") {
        hasChild = true;
      } else if (node.data.name === "region2") {
        hasChild = false;
      } else {
        hasChild = Math.random() > 0.5;
      }

      setTimeout(() => {
        var data;
        if (hasChild) {
          data = [
            {
              name: "zone" + this.count++,
            },
            {
              name: "zone" + this.count++,
            },
          ];
        } else {
          data = [];
        }

        resolve(data);
      }, 500);
    },
    handleNodeClick() {
      // let res = this.$refs.tree.getCheckedNodes();
      // let arr = [];
      // console.log(res);
      // res.forEach((item) => {
      //   let a = {};
      //   a.id = item.id;
      //   a.label = item.label;
      //   arr.push(a);
      // });
      // this.nodeList = arr;
      // console.log(
      //   this.$refs.tree
      //     .getCheckedKeys()
      //     .concat(this.$refs.tree.getHalfCheckedKeys())
      // );
    },
    submit() {
      alert(JSON.stringify(this.nodeList));
    },
  },
};
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
