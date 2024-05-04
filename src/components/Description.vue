<template>
  <div>
    <input id="description" v-model="text" @input="checkBalance" />
    <div>{{ message }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      text: "",
      balancedMessage: "The text is balanced.",
      unbalancedMessage: "The text is not balanced.",
    };
  },
  methods: {
    isBalanced(text) {
      // You can implement the isBalanced logic here
      // For simplicity, I'll just check if the text contains equal number of opening and closing parenthesis
      let count = 0;
      for (let char of text) {
        if (char === "(" || char === "{" || char === "[") {
          count++;
        } else if (char === ")" || char === "{" || char === "[") {
          count--;
        }
      }
      return count === 0;
    },
    checkBalance() {
      if (this.isBalanced(this.text)) {
        this.message = this.balancedMessage;
      } else {
        this.message = this.unbalancedMessage;
      }
    },
  },
  created() {
    this.checkBalance(); // Check initial balance state
  },
};
</script>

<style>
/* Add your component styles here */
</style>
