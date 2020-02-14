<template>
  <div class="effect-component-container">
    <h1>Effect component</h1>
    <Rule></Rule>
  </div>
</template>

<script>
import Rule from "./Rule.vue";
export default {
  data() {
    return {
      effects: []
    };
  },
  components: {
    Rule
  },
  props: {
    options: {
      type: Object,
      required: true
    }
  }
};
</script>

<style scoped>
:root {
  --border-color: #ed6c44;
  --node-color: #ccc;
  --child-shadow-color: #5cb85c;
}
* {
  font-size: 20px;
}
.effect-component-container {
  padding: 8px;
  position: relative;
  border-radius: 3px;
  border: 1px solid var(--border-color);
  border-top: 3px solid #d2d6de;
  margin-bottom: 10px;
  /* width: 100%; */
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.1);
  border-top-color: var(--border-color);
  background-color: rgba(255, 255, 255, 0.9);
}
</style>