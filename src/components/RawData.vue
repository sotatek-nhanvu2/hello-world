<template>
  <div class="raw-data">
    <textarea v-model="currentValue" class="tree-input" aria-multiline="true" rows="15"/>
    <button @click="updateText" class="submit">Submit</button>
  </div>
</template>

<script>
  export default {
    name: "RawData",
    data() {
      return {
        currentValue: ''
      }
    },
    methods: {
      updateText() {
        this.$emit('clicked', {value : this.currentValue});
      }
    }
  }
</script>

<style scoped>
  .raw-data {
    display: block;
  }

  .tree-input {
    width: 100%;
  }
  .submit {
    margin-top: 10px;
  }
</style>
