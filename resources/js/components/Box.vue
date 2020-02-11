<template>
  <div class="boxContainer">
    <div class="and-or-template col-xs-12 and-or-first">
      <div class="form-group and-or-top col-xs-12">
        <div class="col-xs-5 text-left" style="padding: 0">
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
      <Rule></Rule>
    </div>
  </div>
</template>
<script>
import Rule from "./Rule.vue";

export default {
  name: "Box",
  components: {
    Rule
  }
};
</script>

<style>
:root {
  --border-color: #ed6c44;
  --node-color: lightgrey;
}
.and-or-template {
  padding: 10px;
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
  border-color: var(--node-color);
  border-style: solid;
}

.and-or-template:before {
  top: -10px;
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