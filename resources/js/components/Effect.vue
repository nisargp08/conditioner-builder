<template>
  <div class="effect-component-container col-xs-12">
    <div class="col-xs-5" style="padding: 0">
      <span class="effect-title">Condition Effects</span>
    </div>
    <div class="col-xs-7 btn-and-or">
      <button
        class="btn btn-xs btn-orange add-rule pull-right effect-add-button"
        @click.prevent="addEffect"
        title="add condition"
      >+ add</button>
    </div>
    <effect-rule
      v-for="(effect,index) in effects"
      :key="effect"
      :id="effect"
      ref="effects"
      :eOptions="eOptions"
      :effects="effects"
      @delete-effect="deleteEffect(index)"
    ></effect-rule>
  </div>
</template>

<script>
import Rule from "./Rule.vue";
import EffectRule from "./EffectRule.vue";

export default {
  data() {
    return {
      effects: []
    };
  },
  created() {
    this.addEffect();
  },
  components: {
    Rule,
    EffectRule
  },
  props: {
    eOptions: {
      type: Object,
      required: true
    }
  },
  methods: {
    addEffect() {
      var id = this.generateEffectId();
      this.effects.push(id);
    },
    deleteEffect(index) {
      this.effects.splice(index, 1);
    },
    generateEffectId() {
      return "xxxxxxxxxxxxxxxx".replace(/[xy]/g, function(c) {
        var r = (Math.random() * 16) | 0,
          v = c == "x" ? r : (r & 0x3) | 0x8;
        return v.toString(16);
      });
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