<template>
  <div>
    <input id="description" v-model="inputText" @input="checkBalance" />
    <div v-if="isBalanced">{{ balancedMessage }}</div>
    <div v-else>{{ unbalancedMessage }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputText: "",
      isBalanced: false,
      balancedMessage: "The text is balanced.",
      unbalancedMessage: "The text is not balanced.",
    };
  },
  methods: {
    checkBalance() {
      this.isBalanced = this.isBalancedParentheses(this.inputText);
    },
    isBalancedParentheses(text) {
      const stack = [];
      const opening = ["(", "[", "{"];
      const closing = [")", "]", "}"];

      for (let char of text) {
        if (opening.includes(char)) {
          stack.push(char);
        } else if (closing.includes(char)) {
          const index = closing.indexOf(char);
          if (stack.length === 0 || stack.pop() !== opening[index]) {
            return false;
          }
        }
      }

      return stack.length === 0;
    },
  },
};
</script>
