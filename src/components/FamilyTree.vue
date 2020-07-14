<template>
  <div>
    Family tree
    <textarea :value="treeText" class="tree-text"></textarea>
    <canvas id="c" class="c"></canvas>
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
        Object.keys(newValue).forEach(function (root) {
          let tree = newValue[root];
          self.buildTree(root, tree);
        });
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
          var nextPadding = padding + "\t";
          self.buildTree(sub, tree[sub], nextPadding);
        });
      }
    }
  }
</script>

<style scoped>
.tree-text {
  height: 300px;
  width: 300px;
}
</style>
