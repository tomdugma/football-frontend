<template>
  <div class="team-full">
    <div :title="id" class="team-title">
      <b> {{ team_name }} </b>
    </div>
      <img width="100" height="150" :src="team_logo">
      <div class="players">
       <h2>Players</h2>   
      <PlayerPreview v-for="player in players" 
                  :key="player.full_name"
                  :fullname="player.full_name"
                  :team_name="player.team_name"
                  :image="player.image"
                  :position="player.position"></PlayerPreview>
          </div>
      <div  class="futureGames">
          <h2>Future Games</h2>  
          <GamePreview v-for="g in future_games"
            :hostTeam="g.hostTeam" 
            :guestTeam="g.guestTeam" 
            :date="g.date_time"
            :key="g.date_time"></GamePreview>
          <p v-if="future_games.length==0">There are no future games to show</p>
      </div>
      <div class="pastGames">
          <h2>Past Games</h2>
          <GamePreview v-for="g in past_games"             
          :hostTeam="g.hostTeam" 
            :guestTeam="g.guestTeam" 
            :date="g.date_time" 
            :key="g.date_time"></GamePreview>
          <p v-if="past_games.length==0">There are no past games to show</p>
      </div>
  </div>
</template>

<script>
export default {
  name: "TeamFullDetails",
  props: {
      team_name: {
        type: String,
        required: true
      },
      team_logo: {
        type: String,
        required: true
      },
      players: {
        type: Array,
        required: true
      },
      past_games: {
        type: Array,
        required: true
      },
      future_games: {
        type: Array,
        required: true
      }
  }, 
  mounted(){
    console.log("team full details mounted")
  } 
};
</script>

<style>
.team-full {
  display: inline-block;
  width: 250px;
  height: 200px;
}

.team-full .team-title {
  text-align: center;
  text-transform: uppercase;
  color:  rgb(111, 197, 157);
}

.team-full .team-content {
  width: 100%;
  overflow: hidden;
}



</style>
