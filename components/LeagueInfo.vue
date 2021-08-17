<template>
    <div class="league-preview">
      <b-card
      img-alt="Image"
      tag="article"
      style="max-width: 20rem;"
      class="mb-2"
    >
      <b-card-title>{{league_name}}</b-card-title>
      <b-card-text>
        Season: {{ current_season_name }}
        <br/>
        Stage: {{ current_stage_name }}
        <br/>
        <br/>
          <GamePreview
            :hostTeam="game_details.home_team_name" 
            :guestTeam="game_details.guest_team_name" 
            :date="game_details.date_time" 
            >
          </GamePreview>
      </b-card-text>
      <!-- <b-button href="#" variant="primary">Go somewhere</b-button> -->
    </b-card>
  </div>
</template>

<script>

import GamePreview from "./GamePreview.vue";
export default {
name : "LeagueInfo",
  components: {
    GamePreview,
  },
 data() {
    this.getDetails(); 
    return {
      league_name: "", 
      current_season_name: "", 
      current_stage_name: "",
      game_details: {
        date_time: undefined,
        home_team_name: "",
      guest_team_name: ""
      }
    };
  },
    methods: {
    async getDetails() {
      try {
        const response = await this.axios.get(
          `http://localhost:3000/league/getDetails`
        );
        this.league_name = response.data.league_name;
        this.current_season_name = response.data.current_season_name;
        this.current_stage_name = response.data.current_stage_name;
        let game_data = response.data.game_details[0];
        //console.log(game_data);
        // let home_team_details = await this.axios.get(
        //   `http://localhost:3000/teams/teamFullDetails/${game_data.home_team_id}`,
        //   {}
        //   );
        // let guest_team_details = await this.axios.get(
        //   `http://localhost:3000/teams/teamFullDetails/${game_data.guest_team_id}`,
        //   {}
        //   );
        // console.log(home_team_details);
        let game_date_time = game_data.game_date_time;
        let game_home_team = game_data.home_team_id;
        let game_guest_team = game_data.guest_team_id;
        this.game_details = {
          date_time: game_date_time,
          //home_team_name: home_team_details.data.team_name,
          //guest_team_name: guest_team_details.data.team_name,
          home_team_name: game_home_team,
          guest_team_name: game_guest_team
          };
         // console.log(this.game_details);
      } catch (err) {
        console.log(err.response);
      }
    },
  },
    mounted(){
    console.log("league details mounted");
  }
}
</script>

<style>
.league-preview {
  width: 250px;
  height: 200px;
  position: relative;
}

.league-preview .league-title {
  text-align: center;
  text-transform: uppercase;
  color:  rgb(111, 155, 197);
}

.league-preview .league-content {
  width: 100%;
  overflow: hidden;
}

</style>