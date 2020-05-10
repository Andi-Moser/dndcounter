<template>
  <div class="input-group">
        <span class="input-group-btn">
          <button type="button" class="btn btn-default btn-number" data-type="minus" v-on:click="down">
            <span class="fa fa-minus"></span>
          </button>
        </span>
    <input type="text" name="" class="form-control input-number" v-on:input="update($event.target.value)" v-bind:value="value" v-bind:min="0">
    <span class="input-group-btn">
          <button type="button" class="btn btn-default btn-number" data-type="plus" v-on:click="up">
            <span class="fa fa-plus"></span>
          </button>
        </span>
  </div>
</template>

<script>
export default {
  name: 'NumberCounter',
  props: {
    value: Number
  },
  methods: {
    up: function() {
      this.update(this.value + 1);
    },
    down: function() {
      if (parseInt(this.value) > 0) {
        this.update(this.value - 1);
      }
    },
    update: function(value) {
      value = parseInt(value);
      this.$emit("input", value);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
