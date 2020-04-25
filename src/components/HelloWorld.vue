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
  components: {FamilyTree,RawData},
  data () {
    return {
      data: {}
    }
  },
  methods: {
    onClickChild (data) {
      this.data = data;
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
