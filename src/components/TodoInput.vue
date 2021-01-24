<template>
  <div class="input--container">
    <el-input
      @change="handleChange"
      v-model="input"
      placeholder="Enter a todo"
    />
    <el-button
      class="button__item"
      type="success"
      @click="addThisTodo"
      icon="el-icon-check"
    />
  </div>
</template>
<script>
export default {
  name: "TodoInput",
  data() {
    return {
      input: "",
    };
  },
  methods: {
    handleChange() {
      console.log(this.input);
      this.$emit("handleTextChange", this.input);
    },
    addThisTodo() {
      this.$emit("addThisTodo", this.input);
      this.input = "";
    },
  },
};
</script>
