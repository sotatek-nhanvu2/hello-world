<template>
  <div>
    Family tree
  </div>
</template>

<script>
  export default {
    name: "FamilyTree",
    props: ["value"],
    watch: {
      // eslint-disable-next-line no-unused-vars
      'value.relations': function (newValue, oldValue) {
        // eslint-disable-next-line no-debugger
        Object.keys(newValue).forEach(function (root) {
          let tree = newValue[root];
          this.buildTree(root, tree);
        });
      }
    },
    methods: {
      // eslint-disable-next-line no-unused-vars
      buildTree(root, tree) {

      }
    }
  }
</script>

<style scoped>

</style>
