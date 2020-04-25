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
      value: function (newValue, oldValue) {
        console.log("value:\t" + newValue.value);
      }
    }
  }
</script>

<style scoped>

</style>
