<template>
  <div>
    <textarea :value="treeText" class="tree-text"></textarea>
  </div>
</template>

<script>
  export default {
    name: "FamilyTree",
    props: ["value"],
    components: {},
    data() {
      return {
        treeText: ""
      };
    },
    watch: {
      // eslint-disable-next-line no-unused-vars
      'value': function (newValue, oldValue) {
        var self = this;
        this.treeText = "";
        // eslint-disable-next-line no-debugger
        // Object.keys(newValue).forEach(function (root) {
        //   let tree = newValue[root];
        //   self.buildTree(root, tree);
        // });
        self.buildVertical(newValue);
      }
    },
    mounted() {
      let mapScript = document.createElement('script');
      mapScript.setAttribute('src', 'http://cdnjs.cloudflare.com/ajax/libs/fabric.js/3.6.3/fabric.min.js');
      document.head.appendChild(mapScript);
    },
    methods: {
      buildTree(root, tree, padding) {
        padding = padding ? padding : "";
        this.treeText += padding + root + "\n";
        var self = this;
        Object.keys(tree).forEach(function (sub) {
          var nextPadding = padding + "\t\t";
          self.buildTree(sub, tree[sub], nextPadding);
        });
      },
      buildVertical(parents) {
        var titles = [];
        var nextLines = {};
        Object.keys(parents).forEach(parent => {
          titles.push(parent);
          Object.keys(parents[parent]).forEach(sub => {
            nextLines[sub] = parents[parent][sub];
          });
        });
        this.treeText += titles.join("\t\t") + "\n";
        this.buildVertical(nextLines);
      }
    }
  }
</script>

<style scoped>
.tree-text {
  height: 500px;
  width: 100%;
}
</style>
