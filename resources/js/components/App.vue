<template>
  <div class="appContainer">
    <div class="col-xs-8 col-xs-offset-2" style="margin-top: 40px">
      <Box ref="box" v-bind:isFirst="isFirst" v-bind:options="options"></Box>
    </div>
  </div>
</template>

<script>
// Rule - if conditions
//Group - Nested condition boxes
import Box from "./Box.vue";
export default {
  name: "app",
  components: {
    Box
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
      this.$refs.box.addGroup();
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
