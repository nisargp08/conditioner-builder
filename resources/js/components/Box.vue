<template>
  <div class="boxContainer">
    <div class="and-or-template col-xs-12" v-bind:class="[isFirst ? 'and-or-first' : '']">
      <div class="form-group and-or-top col-xs-12">
        <div class="col-xs-5" style="padding: 0">
          <button
            class="btn btn-xs btn-orange-outline btn-radius"
            :class=" isAnd ? 'btn-orange-outline-focus' : '' "
            @click.prevent="clickAnd"
          >&nbsp;All&nbsp;</button>
          <button
            class="btn btn-xs btn-orange-outline btn-radius"
            :class=" !isAnd ? 'btn-orange-outline-focus' : '' "
            @click.prevent="clickOr"
          >&nbsp;Any&nbsp;</button>
        </div>
        <div class="col-xs-7 btn-and-or">
          <button
            v-if="!isFirst"
            class="btn btn-xs btn-orange pull-right"
            @click.prevent="deleteSelf()"
            title="Delete group"
          >
            <i class="fa fa-fw fa-close"></i>
          </button>
          <button
            v-if="showChildButton"
            class="btn btn-xs btn-success add-rule pull-right"
            @click.prevent="showChild"
            title="To display highlighting border around all the child elements"
          >Show Child</button>
          <button
            v-else-if="changeChildButtonText"
            class="btn btn-xs btn-danger add-rule pull-right"
            @click.prevent="showChild"
            title="To remove the highlighting border around all the child elements"
          >Hide Child</button>
          <button
            class="btn btn-xs btn-orange pull-right"
            @click.prevent="addGroup"
            title="add condition group"
          >+ ( group )</button>
          <button
            class="btn btn-xs btn-orange add-rule pull-right"
            @click.prevent="addRule"
            title="add condition"
          >+ add</button>
        </div>
      </div>
      <!-- Rule Starts -->
      <div class="ruleContainer" v-bind:class="isFirst ? ['col-xs-12','group-first'] : ''">
        <Rule
          v-for="(rule,index) in rules"
          ref="rules"
          :key="rule"
          :id="rule"
          v-bind:options="options"
          @delete-rule="deleteRule(index)"
        ></Rule>
      </div>
      <Box
        class="and-or-offset col-xs-11"
        v-for="(group, index) in groups"
        ref="groups"
        :id="group"
        :options="options"
        :key="group"
        @delete-group="deleteGroup(index)"
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
      isAnd: true,
      isShowChild: false
    };
  },
  computed: {
    showChildButton() {
      let result = false;
      if (
        !this.isFirst &&
        this.groups.length >= 1 &&
        this.isShowChild == false
      ) {
        result = true;
      }
      return result;
    },
    changeChildButtonText() {
      let result = false;
      if (
        !this.isFirst &&
        this.groups.length >= 1 &&
        this.isShowChild == true
      ) {
        result = true;
      }
      return result;
    }
  },
  methods: {
    clickAnd() {
      this.isAnd = true;
    },

    clickOr() {
      this.isAnd = false;
    },
    showChild() {
      //Toggle value
      this.isShowChild = !this.isShowChild;
      if (this.isShowChild) {
        for (let i = 0; i < this.groups.length; i++) {
          var id = this.groups[i];
          $("#" + id).addClass("child-box-shadow");
        }
      } else {
        for (let i = 0; i < this.groups.length; i++) {
          var id = this.groups[i];
          $("#" + id).removeClass("child-box-shadow");
        }
      }
    },
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
    deleteSelf() {
      this.$emit("delete-group");
    },

    deleteRule(index) {
      this.rules.splice(index, 1);
    },

    deleteGroup(index) {
      this.groups.splice(index, 1);
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
  --node-color: #ccc;
  --child-shadow-color: #5cb85c;
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
.and-or-template:after,
.group-first:before,
.group-first:after {
  position: absolute;
  content: "";
  left: -32px;
  width: 31px;
  height: calc(50% + 18px);
  border-color: var(--node-color);
  border-style: solid;
}
/*Horizontal lines For the first group only*/
.group-first:before {
  border-width: 0 0 2px 2px;
  top: -18px;
  height: calc(50% + 20px);
}
/* Horizontal lines */
.and-or-template:before {
  border-width: 0 0 2px 2px;
  top: -60px;
  height: calc(50% + 60px);
}
/*Vertical lines*/
.and-or-template:after,
.group-first:after {
  border-width: 0 0 0px 2px;
  top: 50%;
}
/*No border for last child and outer box*/
.and-or-first:before,
.and-or-first:after,
.and-or-first .boxContainer:last-of-type .and-or-template:after,
.and-or-template .ruleContainer:last-of-type:after {
  border: none;
}
/*Different node representation for first-group conditions*/
.group-first .and-or-rule:first-child::before {
  border-width: 0px 0px 2px 0px;
}
.group-first:before {
  width: 58px;
  padding: 2px 2px;
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
.group-first {
  padding: 10px;
  position: relative;
  border-radius: 3px;
  border: 1px solid var(--border-color);
  border-top: 3px solid #d2d6de;
  margin-bottom: 20px;
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.1);
  border-top-color: var(--border-color);
  background-color: rgba(255, 255, 255, 0.9);
  margin-left: 45px;
  width: 89.2%;
  padding-top: 25px;
}
.child-box-shadow {
  -webkit-box-shadow: 0px 0px 20px 5px var(--child-shadow-color);
  -moz-box-shadow: 0px 0px 20px 5px var(--child-shadow-color);
  box-shadow: 0px 0px 20px 5px var(--child-shadow-color);
  padding-top: 15px;
  margin-bottom: 10px;
}
</style>