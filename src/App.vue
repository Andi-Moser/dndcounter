<template>
  <div>
      <nav class="navbar navbar-expand-md navbar-dark fixed-top bg-dark">
          <a class="navbar-brand" href="#">DnD Counter Tool v.0.2</a>
          <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarCollapse" aria-controls="navbarCollapse" aria-expanded="false" aria-label="Toggle navigation">
              <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarCollapse">
              <ul class="navbar-nav mr-auto">
                  <li class="nav-item active">
                      <a class="nav-link" href="#">Home</a>
                  </li>
                  <li class="nav-item">
                      <a class="nav-link" href="#">Link</a>
                  </li>
                  <li class="nav-item">
                      <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
                  </li>
              </ul>
          </div>
      </nav>


      <main role="main" class="container">
          <div class="row">
              <div class="col-md-8">
                  <h1>Playerlist</h1>
                  <table class="table">
                     <tr>
                         <th width="5%">#</th>
                         <th width="20%">Player</th>
                         <th width="10%">Ini</th>
                         <th width="55%">Status</th>
                     </tr>

                      <PlayerEntry v-on:selectPlayer="selectPlayer" v-bind:player="player" v-bind:key="player.id" v-for="player in playerSorted" />
                  </table>
              </div>
              <div class="col-md-4">
                  <Player v-if="currentPlayerId" v-bind:player="getSelectedPlayer()" v-on:changestat="changeStat" v-bind:key="currentPlayerId"></Player>
              </div>
          </div>
      </main>
  </div>
</template>

<script>
import PlayerEntry from "./components/PlayerEntry";
import Player from "./components/Player";
export default {
    name: 'App',
    components: {
        PlayerEntry,
        Player
    },
    data: function() {
        return {
            players: [
                {id: "Boindil", ini: 19, status: {dmg: 2, speed: 50}},
                {id: "Vermeer", ini: 21, status: {dmg: 4, speed: 50}},
                {id: "Esteriell", ini: 20, status: {dmg: 0, speed: 20}},
                {id: "Vanfyr", ini: 8, status: {dmg: 0, speed: 30}},
                {id: "Aahn", ini: 4, status: {dmg: 0, speed: 40, poison: true}},
            ],
            currentPlayerId: null,
            playerSorted: []
        }
    },
    mounted: function() {
        this.updateSort();
    },
    computed: {

    },
    methods: {
        updateSort: function() {
            var playerCopy = JSON.parse(JSON.stringify(this.players)),
                sorted = playerCopy.sort(function(a,b) {
                    return a.ini > b.ini;
                }),
                i = 1;

            sorted.forEach(function(value) {
                value.sort = i++;
            });

            console.log(JSON.stringify(this.players));
            console.log(JSON.parse(JSON.stringify(this.players)));
            console.log(JSON.stringify(sorted));

            this.playerSorted = sorted;
        },
        changeStat: function(stat) {
            console.log("changestat", stat);
            this.getSelectedPlayer()[stat[0]] = stat[1];

            if (stat[0] == "id") {
                // if we changed the ID we need to set the currentPlayerId correctly
                this.currentPlayerId = stat[1];
            }

            // retrigger a sort
            this.updateSort();
        },
        selectPlayer: function(id) {
            this.currentPlayerId = id;
        },
        getSelectedPlayer: function() {
            var currentPlayer = null;
            this.players.find(player => {
                if (player.id == this.currentPlayerId) {
                    currentPlayer = player;
                }
            });

            return currentPlayer;
        }
    }
}
</script>

<style>
    body {
        min-height: 75rem;
        padding-top: 4.5rem;
    }
</style>
