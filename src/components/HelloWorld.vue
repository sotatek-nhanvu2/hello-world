<template>
  <div class="hello">
    <family-tree class="family-tree"/>
    <raw-data class="raw-data"/>
  </div>
</template>

<script>
import FamilyTree from "./FamilyTree";
import RawData from "./RawData";

export default {
  name: 'HelloWorld',
  components: {FamilyTree,RawData},
  props: {
    msg: String
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
