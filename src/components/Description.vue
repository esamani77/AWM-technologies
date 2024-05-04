<template>
  <div>
    <input
      id="description"
      v-model="description"
      @input="validateDescription"
    />
    <div v-if="isBalancedResult">{{ balancedMessage }}</div>
    <div v-else>{{ unbalancedMessage }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      description: "",
      balancedMessage: "The text is balanced.",
      unbalancedMessage: "The text is not balanced.",
      isBalancedResult: false,
      debounce: null,
    };
  },
  methods: {
    validateDescription() {
      clearTimeout(this.debounce);
      this.debounce = setTimeout(() => {
        this.isBalancedResult = this.isBalanced();
      }, 100);
    },
    isBalanced() {
      let stack = [];
      let specialCharCount = 0;
      for (let char of this.description) {
        if (char === "(" || char === "[" || char === "{") {
          stack.push(char);
          specialCharCount++;
        } else if (char === ")" || char === "]" || char === "}") {
          if (stack.length === 0) return false;
          let lastChar = stack.pop();
          if (
            (lastChar === "(" && char !== ")") ||
            (lastChar === "[" && char !== "]") ||
            (lastChar === "{" && char !== "}")
          ) {
            return false;
          }
          specialCharCount--;
        }
      }
      return stack.length === 0 && specialCharCount % 2 === 0;
    },
  },
};
</script>
