<template>
  <tr>
    <td>{{ player.sort }}</td>
    <td v-on:click="selectThisPlayer()">{{ player.id }}</td>
    <td>{{ player.ini }}</td>
    <td>
      <span v-bind:class="'badge badge-pill ' + getClassForStatus(name)" v-for="(value, name) in player.status" v-bind:key="name">{{name}}: {{value}}</span>
    </td>
  </tr>
</template>

<script>
export default {
  name: 'PlayerEntry',
  props: {
    player: Object
  },
  methods: {
    getClassForStatus: function(name) {
      if (name == "dmg") {
        return "badge-danger";
      }

      if (name == "speed") {
        return "badge-info";
      }

      if (name == "poison") {
        return "badge-success";
      }
    },
    selectThisPlayer: function() {
      this.$emit("selectPlayer", this.player.id)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .badge {
    margin-right: 5px;
  }
</style>
