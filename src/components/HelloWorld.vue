<template>
    <div class="hello">
        <raw-data class="raw-data" @clicked="onClickChild"/>
        <family-tree class="family-tree" :value="relations"/>
    </div>
</template>

<script>
  import FamilyTree from "./FamilyTree";
  import RawData from "./RawData";

  export default {
    name: 'HelloWorld',
    components: {FamilyTree, RawData},
    data() {
      return {
        maps: {},
        tree: {},
        relations: {},
        countReplace: 0,
      }
    },
    methods: {
      onClickChild(data) {
        this.data = data;
        this.createMaps();
        this.createRelations();
      },
      createMaps() {
        var maps = {};
        var lines = this.data.value.split('\n');
        for (let j = 0; j < lines.length; j++) {
          let parts = lines[j].split(':');
          let father = parts[0].trim();
          if (!maps[father]) {
            maps[father] = {};
          }
          if (parts.length > 1) {
            let childs = parts[1].split(',');
            for (let k = 0; k < childs.length; k++) {
              let child = childs[k].trim();
              maps[father][child] = {};
            }
          }
        }
        console.log(maps);
        this.maps = maps;
      },
      createRelations() {
        var maps = Object.keys(this.maps);
        var root = maps[0];
        this.tree[root] = this.maps[root];
        this.tree[root] = this.recursiveArray(this.tree[root]);
        this.relations = this.tree;
      },
      recursiveArray(destination) {
        var self = this;
        Object.keys(destination).forEach((sub) => {
          if (self.maps[sub]) {
            destination[sub] = self.maps[sub];
          }
          destination[sub] = self.recursiveArray(destination[sub]);
        });
        return destination;
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }

    .hello {
        display: flex
    }

    .family-tree {
        width: 50%
    }

    .raw-data {
        width: 50%
    }
</style>
