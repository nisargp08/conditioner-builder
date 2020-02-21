<template>
  <div class="appContainer">
    <!-- <div class="condition-group col-xs-8 col-xs-offset-2">
      <div class="col-xs-12" style="margin-top: 20px">
        <Box ref="box" v-bind:isFirst="isFirst" v-bind:options="options"></Box>
      </div>
      <div class="effect-container col-xs-12" style="margin-bottom: 20px">
        <effect ref="effect" :eOptions="eOptions"></effect>
      </div>
    </div>-->
    <condition
      v-for="(condition,index) in conditions"
      :key="condition"
      ref="condition"
      :id="condition"
      :cnt="index + 1"
      @delete-condition="deleteCondition(index)"
    ></condition>
    <div class="col-xs-8 col-xs-offset-2">
      <button
        class="btn btn-primary main-button"
        title="Add a new condition"
        @click.prevent="addCondition"
      >Add Condition</button>
      <button class="btn btn-success main-button" title="Save conditions">Save Condition</button>
    </div>
  </div>
</template>

<script>
import Condition from "./Condition.vue";
export default {
  name: "app",
  components: {
    Condition
  },
  data() {
    return {
      conditions: []
    };
  },
  mounted() {
    this.$nextTick(function() {
      //When component mounted
      this.init();
    });
  },
  methods: {
    init() {
      this.addCondition();
    },
    addCondition() {
      var conId = this.generateId();
      this.conditions.push(conId);
    },
    deleteCondition(index) {
      this.conditions.splice(index, 1);
    },
    generateId() {
      return "xxxxxxxxxxxxxxxx".replace(/[xy]/g, function(c) {
        var r = (Math.random() * 16) | 0,
          v = c == "x" ? r : (r & 0x3) | 0x8;
        return v.toString(16);
      });
    }
  }
};
</script>

<style>
body {
  background: linear-gradient(
    to left bottom,
    rgb(125, 148, 175) 0%,
    rgb(230, 111, 31) 100%
  );
}
</style>
