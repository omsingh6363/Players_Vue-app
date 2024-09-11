<!-- PlayerDashboard.vue -->
<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Sportz Interactive</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
                data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false"
                aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <select v-model="selectedTeam" @change="filterPlayers" class="form-select">
              <option value="ALL">ALL</option>
              <option value="IND">IND</option>
              <option value="PAK">PAK</option>
              <option value="AUS">AUS</option>
              <option value="ENG">ENG</option>
            </select>
          </ul>
          <form class="d-flex" role="search">
            <input class="form-control me-2" type="search" placeholder="Search" v-model="searchQuery">
            <button class="btn btn-outline-success" type="button" @click="searchPlayers">Search</button>
          </form>
        </div>
      </div>
    </nav>

    <div class="container">
      <div v-for="(players, role) in groupedPlayers" :key="role" class="role-section">
        <h2 class="role-title">{{ getRoleName(role) }}</h2>
        <div class="player-grid">
          <div v-for="player in players" :key="player.name" class="player-card">
            <div class="card-image">
              <img :src="player.image" :alt="player.name">
            </div>
            <div class="card-content">
              <h3 class="player-name">{{ player.name }}</h3>
              <p class="team-name">{{ player.team_name }}</p>
              <div class="player-stats">
                <p>Matches: {{ player.matches }}</p>
                <p>Runs: {{ player.runs }}</p>
                <p>50s/100s: {{ player['50s'] }}/{{ player['100s'] }}</p>
                <p>Highest: {{ player.highest_score }}</p>
                <p>Best Bowling: {{ player.best_bowling_figures || 'N/A' }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import playersData from '../assets/players.json';

export default {
  name: 'PlayerDashboard',
  data() {
    return {
      players: [],
      selectedTeam: 'ALL',
      searchQuery: '',
      filteredPlayers: []
    };
  },
  computed: {
    groupedPlayers() {
      const grouped = {
        2: [], //batsmen
        3: [], // all-rounders
        4: []  // bowlers
      };
      this.filteredPlayers.forEach(player => {
        grouped[player.role].push(player);
      });
      return grouped;
    }
  },
  methods: {
    loadPlayers() {
      this.players = playersData.originalPlayers;
      this.filteredPlayers = this.players;
    },
    filterPlayers() {
      if (this.selectedTeam === 'ALL') {
        this.filteredPlayers = this.players;
      } else {
        this.filteredPlayers = this.players.filter(player => player.team_name === this.selectedTeam);
      }
    },
    searchPlayers() {
      const query = this.searchQuery.toLowerCase();
      this.filteredPlayers = this.players.filter(player => 
        player.name.toLowerCase().includes(query) ||
        player.team_name.toLowerCase().includes(query)
      );
    },
    getRoleName(role) {
      const roles = {
        2: 'Batsmen',
        3: 'All-rounders',
        4: 'Bowlers'
      };
      return roles[role] || 'Unknown';
    }
  },
  created() {
    this.loadPlayers();
  }
};
</script>

<style scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.role-section {
  margin-bottom: 40px;
}

.role-title {
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 20px;
  color: #333;
  text-align: center;
}

.player-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
}

.player-card {
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  transition: transform 0.3s ease;
}

.player-card:hover {
  transform: translateY(-5px);
}

.card-image {
  height: 200px;
  overflow: hidden;
}

.card-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.card-content {
  padding: 15px;
}

.player-name {
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 5px;
  color: #333;
}

.team-name {
  font-size: 14px;
  color: #666;
  margin-bottom: 10px;
}

.player-stats {
  font-size: 14px;
  color: #444;
}

.player-stats p {
  margin: 5px 0;
}

.form-select {
  width: auto;
  margin-right: 15px;
}

@media (max-width: 768px) {
  .player-grid {
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  }
}
</style>