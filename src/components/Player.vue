<template>
  <div>
    <h2>{{playerObject.id}}</h2>

    <form>
      <div class="form-group">
        <label for="name">Change Name</label>
        <input type="text" class="form-control" id="name" v-model="newName">
      </div>
      <button type="submit" class="btn btn-primary" @click.prevent="saveName">Save</button>

      <h4>Initiative</h4>
      <NumberCounter v-model="playerObject.ini" v-on:input="updateIni" />
    </form>
  </div>
</template>

<script>
import NumberCounter from "./NumberCounter";

export default {
  name: 'Player',
  components: {
    NumberCounter
  },
  props: {
    player: Object
  },
  methods: {
    saveName: function() {
      this.$emit("changestat", ["id", this.newName]);
    },
    updateIni: function(value) {
      this.player.ini = value;
      this.$emit("changestat", ["ini", value]);
    }
  },
  watch: {
  },
  data: function() {
    return {
      playerObject: this.player,
      newName: this.player.id
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
