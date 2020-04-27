<template>
  <div>
    Family tree
    <canvas id="c" class="c"></canvas>
  </div>
</template>

<script>
  export default {
    name: "FamilyTree",
    props: ["value"],
    components: {},
    data() {
      return {};
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
      let mapScript = document.createElement('script');
      mapScript.setAttribute('src', 'http://cdnjs.cloudflare.com/ajax/libs/fabric.js/3.6.3/fabric.min.js');
      document.head.appendChild(mapScript);
    },
    methods: {
      buildTree(root, tree) {
        var canvas = new fabric.Canvas('c', { selection: false });
        fabric.Object.prototype.originX = fabric.Object.prototype.originY = 'center';

        var line = this.makeLine([150, 25, 150, 75]),
          line2 = this.makeLine([150, 75, 150, 150]),
          line3 = this.makeLine([150, 150, 200, 250]),
          line4 = this.makeLine([150, 150, 100, 250]),
          line5 = this.makeLine([150, 75, 75, 125]),
          line6 = this.makeLine([150, 75, 225, 125]);

        canvas.add(line, line2, line3, line4, line5, line6);

        canvas.add(
          this.makeCircle(line.get('x1'), line.get('y1'), null, line),
          this.makeCircle(line.get('x2'), line.get('y2'), line, line2, line5, line6),
          this.makeCircle(line2.get('x2'), line2.get('y2'), line2, line3, line4),
          this.makeCircle(line3.get('x2'), line3.get('y2'), line3),
          this.makeCircle(line4.get('x2'), line4.get('y2'), line4),
          this.makeCircle(line5.get('x2'), line5.get('y2'), line5),
          this.makeCircle(line6.get('x2'), line6.get('y2'), line6)
        );
        canvas.on('object:moving', function (e) {
          var p = e.target;
          p.line1 && p.line1.set({'x2': p.left, 'y2': p.top});
          p.line2 && p.line2.set({'x1': p.left, 'y1': p.top});
          p.line3 && p.line3.set({'x1': p.left, 'y1': p.top});
          p.line4 && p.line4.set({'x1': p.left, 'y1': p.top});
          canvas.renderAll();
        });
      },
      makeCircle(left, top, line1, line2, line3, line4) {
        var c = new fabric.Circle({
          left: left,
          top: top,
          strokeWidth: 5,
          radius: 12,
          fill: '#fff',
          stroke: '#666'
        });
        c.hasControls = c.hasBorders = false;

        c.line1 = line1;
        c.line2 = line2;
        c.line3 = line3;
        c.line4 = line4;

        return c;
      },
      makeLine(coords) {
        return new fabric.Line(coords, {
          fill: 'red',
          stroke: 'red',
          strokeWidth: 5,
          selectable: false,
          evented: false,
        });
      }
    }
  }
</script>

<style scoped>

</style>
