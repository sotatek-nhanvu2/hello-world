<template>
  <div>
    Family tree
    <canvas id="c"></canvas>
    <fabric-canvas>
      <fabric-circle :id="3"></fabric-circle>
      <fabric-circle :id="2"></fabric-circle>
    </fabric-canvas>
  </div>
</template>

<script>
  import vueFabricWrapper from "vue-fabric-wrapper";

  export default {
    name: "FamilyTree",
    props: ["value"],
    components: {
      FabricCanvas: vueFabricWrapper.FabricCanvas,
      FabricCircle: vueFabricWrapper.FabricCircle
    },
    data () {
      return {
        rectWidth: 30,
      }
    },
    watch: {
      // eslint-disable-next-line no-unused-vars
      'value.relations': function (newValue, oldValue) {
        var self = this;
        // eslint-disable-next-line no-debugger
        Object.keys(newValue).forEach(function (root) {
          let tree = newValue[root];
          self.buildTree(root, tree);
        });
      }
    },
    mounted() {
      var c = document.getElementById("c");
      var ctx = c.getContext("2d");
      this.vueCanvas = ctx;
    },
    methods: {
      // eslint-disable-next-line no-unused-vars
      buildTree(root, tree) {
        this.drawRect();
      },
      drawRect() {
        // eslint-disable-next-line no-debugger
        // clear canvas
        this.vueCanvas.clearRect(0, 0, 400, 200);

        // draw rect
        this.vueCanvas.beginPath();
        this.vueCanvas.rect(20, 20, this.rectWidth, 100);
        this.vueCanvas.stroke();
      },
      addWidth() {
        this.rectWidth += 10;
        this.drawRect()
      },
      subWidth() {
        this.rectWidth -= 10;
        this.drawRect()
      }
    }
  }
</script>

<style scoped>

</style>
