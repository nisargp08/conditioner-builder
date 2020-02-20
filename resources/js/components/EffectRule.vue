<template>
  <div class="effect-rules">
    <div class="form-group col-xs-12">
      <div class="col-xs-3">
        <select class="form-control input-sm">
          <option
            v-for="(effect,index) in eOptions.operator"
            :key="index"
            :value="effect.id"
          >{{ effect.name }}</option>
        </select>
      </div>
      <div class="col-xs-3">
        <select class="form-control input-sm">
          <option
            v-for="(effect,index) in eOptions.firstSelector"
            :key="index"
            :value="effect.id"
          >{{ effect.name }}</option>
        </select>
      </div>
      <div class="col-xs-3">
        <select class="form-control input-sm">
          <option
            v-for="(effect,index) in eOptions.secondSelector"
            :key="index"
            :value="effect.id"
          >{{ effect.name }}</option>
        </select>
      </div>
      <button
        v-if="effectLength"
        @click="deleteSelf()"
        class="btn btn-xs btn-orange-outline btn-radius btn-orange-round btn-cancel"
      >
        <i class="fa fa-fw fa-close"></i>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "effect-rules",
  props: ["eOptions", "effects"],
  methods: {
    deleteSelf() {
      this.$emit("delete-effect");
    }
  },
  computed: {
    effectLength() {
      var result = false;
      if (this.effects.length > 1) {
        //Show delete(x) button
        return true;
      }
      return result;
    }
  }
};
</script>
<style scoped>
</style>