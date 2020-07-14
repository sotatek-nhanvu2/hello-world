<template>
  <div class="hello">
    <raw-data class="raw-data" @clicked="onClickChild"/>
    <family-tree class="family-tree" :value="data"/>
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
        data: {
          countReplace: 0
        }
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
        this.data.maps = maps;
      },
      createRelations () {
        var maps = this.data.maps;
        this.data.relations = this.sort(maps);
      },
      sort(maps) {
        var self = this;
        this.countReplace = 0;
        Object.keys(maps).forEach(function (parent) {
          if (!maps[parent]) {
            return;
          }
          var childs = maps[parent];
          maps[parent] = self.replace(childs, maps, maps[parent]);
        });
        if (this.countReplace > 0) {
          this.sort(maps);
        }
        return maps;
      },
      replace (childs, compares, destination) {
        var self = this;
        Object.keys(childs).forEach(function (child) {
          if (compares[child]) {
            destination[child] = compares[child];
            delete compares[child];
            self.countReplace++;
          }
          Object.keys(destination[child]).forEach(function (subChild) {
            if (compares[subChild]) {
              destination[child][subChild] = compares[subChild];
              delete compares[subChild];
              self.countReplace++;
            }
          });
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
