<template>
  <div class="form-group and-or-rule col-xs-12">
    <div class="col-xs-3">
      <select class="form-control input-sm" v-model="firstSelector">
        <option
          v-for="(option,index) in options.firstSelector"
          :key="index"
          :value="option.id"
        >{{ option.name }}</option>
      </select>
    </div>
    <div class="col-xs-3">
      <select class="form-control input-sm" v-model="operator">
        <option
          v-for="(option,index) in options.operator"
          :key="index"
          :value="option.id"
        >{{ option.name }}</option>
      </select>
    </div>
    <div class="col-xs-3">
      <select class="form-control input-sm" v-model="secondSelector">
        <option
          v-for="(option,index) in options.secondSelector"
          :key="index"
          :value="option.id"
        >{{ option.name }}</option>
      </select>
    </div>
    <button
      class="btn btn-xs btn-purple-outline btn-radius btn-purple-round btn-cancel"
      @click.prevent="deleteSelf()"
    >
      <i class="fa fa-fw fa-close"></i>
    </button>
  </div>
  <!-- First Panel -->
  <!-- <div class="panel panel-default initial-rule-card and-or-template">
      <div class="panel-body">
        <div class="form-group">
          <div class="col-xs-4">
            <select class="form-control input-sm">
              <option>Condition Selector 1</option>
              <option>Condition Selector 2</option>
              <option>Condition Selector 3</option>
              <option>Condition Selector 4</option>
              <option>Condition Selector 5</option>
            </select>
          </div>
          <div class="col-xs-2">
            <select class="form-control input-sm">
              <option>Condition Selector 1</option>
              <option>Condition Selector 2</option>
              <option>Condition Selector 3</option>
              <option>Condition Selector 4</option>
              <option>Condition Selector 5</option>
            </select>
          </div>
          <div class="col-xs-4">
            <select class="form-control input-sm">
              <option>Condition Selector 1</option>
              <option>Condition Selector 2</option>
              <option>Condition Selector 3</option>
              <option>Condition Selector 4</option>
              <option>Condition Selector 5</option>
            </select>
          </div>
          <div class="col-xs-2 btn-cancel">
            <button class="btn btn-xs btn-purple-outline btn-radius btn-purple-round btn-cancel">
              <i class="fa fa-fw fa-close"></i>
            </button>
          </div>
        </div>
        <div class="form-group">
          <div class="col-xs-4">
            <select class="form-control input-sm">
              <option>Condition Selector 1</option>
              <option>Condition Selector 2</option>
              <option>Condition Selector 3</option>
              <option>Condition Selector 4</option>
              <option>Condition Selector 5</option>
            </select>
          </div>
          <div class="col-xs-2">
            <select class="form-control input-sm">
              <option>Condition Selector 1</option>
              <option>Condition Selector 2</option>
              <option>Condition Selector 3</option>
              <option>Condition Selector 4</option>
              <option>Condition Selector 5</option>
            </select>
          </div>
          <div class="col-xs-4">
            <select class="form-control input-sm">
              <option>Condition Selector 1</option>
              <option>Condition Selector 2</option>
              <option>Condition Selector 3</option>
              <option>Condition Selector 4</option>
              <option>Condition Selector 5</option>
            </select>
          </div>
          <div class="col-xs-2 btn-cancel">
            <button class="btn btn-xs btn-purple-outline btn-radius btn-purple-round btn-cancel">
              <i class="fa fa-fw fa-close"></i>
            </button>
          </div>
        </div>
        <div class="form-group">
          <div class="col-xs-4">
            <select class="form-control input-sm">
              <option>Condition Selector 1</option>
              <option>Condition Selector 2</option>
              <option>Condition Selector 3</option>
              <option>Condition Selector 4</option>
              <option>Condition Selector 5</option>
            </select>
          </div>
          <div class="col-xs-2">
            <select class="form-control input-sm">
              <option>Condition Selector 1</option>
              <option>Condition Selector 2</option>
              <option>Condition Selector 3</option>
              <option>Condition Selector 4</option>
              <option>Condition Selector 5</option>
            </select>
          </div>
          <div class="col-xs-4">
            <select class="form-control input-sm">
              <option>Condition Selector 1</option>
              <option>Condition Selector 2</option>
              <option>Condition Selector 3</option>
              <option>Condition Selector 4</option>
              <option>Condition Selector 5</option>
            </select>
          </div>
          <div class="col-xs-2 btn-cancel">
            <button class="btn btn-xs btn-purple-outline btn-radius btn-purple-round btn-cancel">
              <i class="fa fa-fw fa-close"></i>
            </button>
          </div>
        </div>
        <div class="form-group">
          <div class="col-xs-4">
            <select class="form-control input-sm">
              <option>Condition Selector 1</option>
              <option>Condition Selector 2</option>
              <option>Condition Selector 3</option>
              <option>Condition Selector 4</option>
              <option>Condition Selector 5</option>
            </select>
          </div>
          <div class="col-xs-2">
            <select class="form-control input-sm">
              <option>Condition Selector 1</option>
              <option>Condition Selector 2</option>
              <option>Condition Selector 3</option>
              <option>Condition Selector 4</option>
              <option>Condition Selector 5</option>
            </select>
          </div>
          <div class="col-xs-4">
            <select class="form-control input-sm">
              <option>Condition Selector 1</option>
              <option>Condition Selector 2</option>
              <option>Condition Selector 3</option>
              <option>Condition Selector 4</option>
              <option>Condition Selector 5</option>
            </select>
          </div>
          <div class="col-xs-2 btn-cancel">
            <button class="btn btn-xs btn-purple-outline btn-radius btn-purple-round btn-cancel">
              <i class="fa fa-fw fa-close"></i>
            </button>
          </div>
        </div>
      </div>
  </div>-->
</template>
<script>
// Rule - if conditions
//Group - Nested condition boxes
export default {
  name: "rule",
  props: ["options"],
  methods: {
    deleteSelf() {
      this.$emit("delete-rule");
    }
  }
};
</script>

<style>
:root {
  --node-color: grey;
}

.and-or-rule {
  position: relative;
  height: 30px;
  margin-left: 15px !important;
  padding-left: 0;
}

/* .and-or-rule:before,
.and-or-rule:after {
  content: "";
  position: absolute;
  left: -1px;
  width: 16px;
  height: calc(50% + 15px);
  border-color: #ccc;
  border-style: solid;
}

.and-or-rule:before {
  top: -15px;
  border-width: 0 0 2px 2px;
}

.and-or-rule:after {
  top: 50%;
  border-width: 0 0 0 2px;
}

.and-or-rule:last-child:after {
  border: none;
} */
</style>