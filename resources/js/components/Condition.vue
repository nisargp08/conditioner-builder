<template>
  <div class="condition-group col-xs-8 col-xs-offset-2" :id="id">
    <div class="panel panel-default" style="margin-top: 20px">
      <div class="panel-heading">
        <span class="collapse-caret">
          <button
            data-toggle="collapse"
            aria-controls="condition-collapse"
            aria-expanded="false"
            :href="'#body-' + id"
            :class="[!isCollapsed ? 'fa fa-chevron-circle-down' : 'fa fa-chevron-circle-right']"
            :title="[!isCollapsed ? 'Collapse the condition container' : 'Show collapsed condition container']"
            @click.prevent="collapseClicked"
          ></button>
        </span>
        <span class="vertical-divider"></span>
        <span class="condition-header">Condition - {{cnt}}</span>
        <span class="condition-delete float-right">
          <button title="Delete condition" @click.prevent="deleteSelf()">
            <i class="fa fa-trash" aria-hidden="true"></i>
          </button>
        </span>
      </div>
      <div class="collapse in show panel-body" :id="'body-' + id">
        <div class="group-container col-xs-12">
          <Box ref="box" v-bind:isFirst="isFirst" v-bind:options="options"></Box>
        </div>
        <div class="effect-container col-xs-12">
          <effect ref="effect" :eOptions="eOptions"></effect>
        </div>
        <div class="col-xs-12" style="margin-bottom:20px">
          <button
            class="btn btn-danger pull-right"
            title="Delete the condition block"
            @click.prevent="deleteSelf()"
          >
            <i class="fa fa-fw fa-close fa-2x"></i>
            <span class="deleteText">Delete</span>
          </button>
        </div>
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
  props: ["cnt", "id"],
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
      isFirst: true,
      isCollapsed: false
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
    },
    collapseClicked() {
      this.isCollapsed = !this.isCollapsed;
    },
    deleteSelf() {
      this.$emit("delete-condition");
    }
  }
};
</script>
<style scoped>
.deleteText {
  font-size: 1.5rem;
}
.panel-heading {
  font-size: 2rem;
  font-weight: 600;
  padding-left: 0px;
}
.vertical-divider {
  border-left: 1px solid grey;
  padding-right: 8px;
}
.collapse-caret {
  padding-left: 5px;
}
.collapse-caret button,
.collapse-caret button:focus,
.collapse-caret button:active {
  border: none;
}
.collapse-caret button {
  width: 50px;
  background-color: white;
}
.condition-delete {
  color: red;
  background-color: gainsboro;
  border-radius: 5px;
}
.condition-delete button {
  background-color: gainsboro;
  padding-left: 10px;
  padding-right: 10px;
  border-radius: 5px;
  border: none;
}
</style>
