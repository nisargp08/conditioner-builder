<template>
  <div class="boxContainer">
    <div class="and-or-template col-xs-12" v-bind:class="isFirst ? 'and-or-first' : ''">
      <div class="form-group and-or-top col-xs-12">
        <div class="col-xs-5" style="padding: 0">
          <button class="btn btn-xs btn-purple-outline btn-radius">&nbsp;And&nbsp;</button>
          <button class="btn btn-xs btn-purple-outline btn-radius">&nbsp;Or&nbsp;</button>
        </div>
        <div class="col-xs-7 btn-and-or">
          <button class="btn btn-xs btn-purple pull-right">
            <i class="fa fa-fw fa-close"></i>
          </button>
          <button class="btn btn-xs btn-purple pull-right">+ ( group )</button>
          <button class="btn btn-xs btn-purple add-rule pull-right">+ add</button>
        </div>
      </div>
      <!-- Rule Starts -->
      <Rule v-for="(rule,index) in rules" ref="rules" :key="rule" v-bind:options="options"></Rule>
      <Box
        class="and-or-offset col-xs-11"
        v-for="(group, index) in groups"
        ref="groups"
        :options="options"
        :key="group"
      ></Box>
    </div>
  </div>
</template>
<script>
import Rule from "./Rule.vue";

export default {
  // Rule - if conditions
  //Group - Nested condition boxes

  name: "Box",
  components: {
    Rule
  },
  created() {
    this.addRule();
  },
  //Passed property values from the previous component -- in our case App.Vue
  props: {
    options: {
      type: Object,
      required: true
    },
    isFirst: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      //Storing is/isnot condition
      rules: [],
      //Storing nested groups
      groups: [],
      //To keep track if logical gate 'AND' is selected or not -- By default set to true
      isAnd: true
    };
  },
  methods: {
    addRule() {
      //Generating unique random id
      var id = this.generateId();
      //Adding a new rule to the array
      this.rules.push(id);
    },
    addGroup() {
      var id = this.generateId();
      this.groups.push(id);
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
:root {
  --border-color: #ed6c44;
  --node-color: lightgrey;
}
.and-or-template {
  /* padding: 10px; */
  padding: 8px;
  position: relative;
  border-radius: 3px;
  border: 1px solid var(--border-color);
  border-top: 3px solid #d2d6de;
  margin-bottom: 20px;
  /* width: 100%; */
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.1);
  border-top-color: var(--border-color);
  background-color: rgba(255, 255, 255, 0.9);
}

.and-or-template:before,
.and-or-template:after {
  content: "";
  position: absolute;
  left: -17px;
  width: 16px;
  height: calc(50% + 18px);
  /* left: -36px;
  width: 35px;
  height: calc(50% + 32px); */
  border-color: var(--node-color);
  border-style: solid;
}

.and-or-template:before {
  top: -18px;
  /* top: -32px; */
  border-width: 0 0 2px 2px;
}

.and-or-template:after {
  top: 50%;
  border-width: 0 0 0 2px;
}

.and-or-first:before,
.and-or-first:after,
.and-or-template:last-child:after {
  border: none;
}

.and-or-top,
.btn-and-or {
  padding: 0;
}

.btn-and-or button {
  margin-left: 4px;
}

.and-or-offset {
  margin-left: 30px;
}
</style>