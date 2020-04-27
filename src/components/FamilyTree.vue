<template>
  <div>
    Family tree
    <fabric-canvas :height="400" :width="400">
      <fabric-line :id="'headToBody'" :x1="headPosLeft" :y1="headPosTop" :x2="bodyPosLeft" :y2="bodyPosTop" :fill="'red'" :stroke="'red'" :strokeWidth="5" :selectable="false" :evented="false" :originX="'center'" :originY="'center'"></fabric-line>
      <fabric-line :id="'bodyToWaist'" :x1="bodyPosLeft" :y1="bodyPosTop" :x2="waistPosLeft" :y2="waistPosTop" :fill="'red'" :stroke="'red'" :strokeWidth="5" :selectable="false" :evented="false" :originX="'center'" :originY="'center'"></fabric-line>
      <fabric-line :id="'bodyToLeftArm'" :x1="bodyPosLeft" :y1="bodyPosTop" :x2="leftHandPosLeft" :y2="leftHandPosTop" :fill="'red'" :stroke="'red'" :strokeWidth="5" :selectable="false" :evented="false" :originX="'center'" :originY="'center'"></fabric-line>
      <fabric-line :id="'bodyToRightArm'" :x1="bodyPosLeft" :y1="bodyPosTop" :x2="rightHandPosLeft" :y2="rightHandPosTop" :fill="'red'" :stroke="'red'" :strokeWidth="5" :selectable="false" :evented="false" :originX="'center'" :originY="'center'"></fabric-line>
      <fabric-line :id="'waistToLeftFoot'" :x1="leftFootPosLeft" :y1="leftFootPosTop" :x2="waistPosLeft" :y2="waistPosTop" :fill="'red'" :stroke="'red'" :strokeWidth="5" :selectable="false" :evented="false" :originX="'center'" :originY="'center'"></fabric-line>
      <fabric-line :id="'waistToRightFoot'" :x1="rightFootPosLeft" :y1="rightFootPosTop" :x2="waistPosLeft" :y2="waistPosTop" :fill="'red'" :stroke="'red'" :strokeWidth="5" :selectable="false" :evented="false" :originX="'center'" :originY="'center'"></fabric-line>
      <fabric-rectangle :id="'head'" :left.sync="headPosLeft" :top.sync="headPosTop" :strokeWidth="5" :radius="12" :fill="'#fff'" :stroke="'#666'" :originX="'center'" :originY="'center'"></fabric-rectangle>
      <fabric-rectangle :id="'body'" :left.sync="bodyPosLeft" :top.sync="bodyPosTop" :strokeWidth="5" :radius="12" :fill="'#fff'" :stroke="'#666'" :originX="'center'" :originY="'center'"></fabric-rectangle>
      <fabric-rectangle :id="'waist'" :left.sync="waistPosLeft" :top.sync="waistPosTop" :strokeWidth="5" :radius="12" :fill="'#fff'" :stroke="'#666'" :originX="'center'" :originY="'center'"></fabric-rectangle>
      <fabric-rectangle :id="'leftHand'" :left.sync="leftHandPosLeft" :top.sync="leftHandPosTop" :strokeWidth="5" :radius="12" :fill="'#fff'" :stroke="'#666'" :originX="'center'" :originY="'center'"></fabric-rectangle>
      <fabric-rectangle :id="'rightHand'" :left.sync="rightHandPosLeft" :top.sync="rightHandPosTop" :strokeWidth="5" :radius="12" :fill="'#fff'" :stroke="'#666'" :originX="'center'" :originY="'center'"></fabric-rectangle>
      <fabric-rectangle :id="'leftFoot'" :left.sync="leftFootPosLeft" :top.sync="leftFootPosTop" :strokeWidth="5" :radius="12" :fill="'#fff'" :stroke="'#666'" :originX="'center'" :originY="'center'"></fabric-rectangle>
      <fabric-rectangle :id="'rightFoot'" :left.sync="rightFootPosLeft" :top.sync="rightFootPosTop" :strokeWidth="5" :radius="12" :fill="'#fff'" :stroke="'#666'" :originX="'center'" :originY="'center'"></fabric-rectangle>
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
      FabricRectangle: vueFabricWrapper.FabricRectangle,
      FabricLine: vueFabricWrapper.FabricLine
    },
    data() {
      return {
        leftHandPosLeft: 175,
        rightHandPosLeft: 325,
        leftFootPosLeft: 200,
        rightFootPosLeft: 300,
        headPosLeft: 250,
        bodyPosLeft: 250,
        waistPosLeft: 250,

        headPosTop: 50,
        bodyPosTop: 150,
        waistPosTop: 250,
        leftHandPosTop: 250,
        rightHandPosTop: 250,
        leftFootPosTop: 350,
        rightFootPosTop: 350
      };
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

    },
    methods: {
      // eslint-disable-next-line no-unused-vars
      buildTree(root, tree) {

      },
    }
  }
</script>

<style scoped>

</style>
