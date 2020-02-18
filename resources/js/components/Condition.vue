<template>
  <div class="condition-group col-xs-8 col-xs-offset-2">
    <div class="col-xs-12" style="margin-top: 20px">
      <Box ref="box" v-bind:isFirst="isFirst" v-bind:options="options"></Box>
      <div class="effect-container col-xs-12" style="margin-bottom: 20px">
        <effect ref="effect" :eOptions="eOptions"></effect>
      </div>
    </div>
  </div>
</template>

<script>
// Rule - if conditions
//Group - Nested condition boxes
import Box from "./Box.vue";
import Effect from "./Effect.vue";
export default {
  name: "condition",
  components: {
    Box,
    Effect
  },
  data() {
    return {
      //Dropdown field values object
      options: {
        firstSelector: [
          {
            id: 1,
            name: "Name"
          },
          {
            id: 2,
            name: "Age"
          },
          {
            id: 3,
            name: "Phone"
          },
          {
            id: 4,
            name: "Email"
          },
          {
            id: 5,
            name: "Password"
          }
        ],
        operator: [
          {
            id: "is",
            name: "is"
          },
          {
            id: "isnot",
            name: "is not"
          }
        ],
        secondSelector: [
          {
            id: 6,
            name: "Name Tester"
          },
          {
            id: 7,
            name: "Age Tester"
          },
          {
            id: 8,
            name: "Phone Tester"
          },
          {
            id: 9,
            name: "Email Tester"
          },
          {
            id: 10,
            name: "Password Tester"
          }
        ]
      },
      //Dropdown field values for effect
      eOptions: {
        firstSelector: [
          {
            id: 1,
            name: "Name"
          },
          {
            id: 2,
            name: "Age"
          },
          {
            id: 3,
            name: "Phone"
          },
          {
            id: 4,
            name: "Email"
          },
          {
            id: 5,
            name: "Password"
          }
        ],
        operator: [
          {
            id: 6,
            name: "Show"
          },
          {
            id: 7,
            name: "Hide"
          },
          {
            id: 8,
            name: "Make Required"
          },
          {
            id: 9,
            name: "Auto Deselect/Clear Field"
          },
          {
            id: 10,
            name: "Make Readonly"
          },
          {
            id: 11,
            name: "Make Editable"
          }
        ],
        secondSelector: [
          {
            id: 12,
            name: "Name Tester"
          },
          {
            id: 13,
            name: "Age Tester"
          },
          {
            id: 14,
            name: "Phone Tester"
          },
          {
            id: 15,
            name: "Email Tester"
          },
          {
            id: 16,
            name: "Password Tester"
          }
        ]
      },
      //Indicates if the div is first group or not
      isFirst: true
    };
  },
  mounted() {
    //Calling Initi function to display by default condition when the componets gets mounted
    this.$nextTick(function() {
      this.init();
    });
  },
  methods: {
    init() {
      this.$refs.box.addRule();
      this.$refs.box.addGroup();
      //   this.$refs.box.addGroup();
    }
  }
};
</script>

<style scoped>
.effect-container {
  padding: 0;
}
</style>
