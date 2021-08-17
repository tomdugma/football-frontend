<template>
<div v-if="games.length ==0"> No favorite games to show</div>
  <div v-else>
    <GamePreview
      v-for="g in games"
      :hostTeam="g.home_team_name" 
      :guestTeam="g.guest_team_name" 
      :date="g.date_time" 
      :key="g.id">
      </GamePreview>
      </div>
</template>

<script>
import GamePreview from "./GamePreview.vue";
export default {
  name: "FavoriteGames",
  components: {
    GamePreview
  }, 
  data() {
    this.updateGames();
    return {
      games: []
      //[
  //       {
  //         id:25,
  //         hostTeam: "Maccabi Tel-Aviv",
  //         guestTeam: "Hapoel Beer-Sheva",
  //         date: "27/5/21",
  //         hour: "20:00"
  //       },
  //       {
  //         id:39,
  //         hostTeam: "Hapoel Tel-Aviv",
  //         guestTeam: "Maccabi Haifa",
  //         date: "29/5/21",
  //         hour: "20:00"
  //       }
  //     ]
    
     };
   },
  methods: {
    updateGames(){
    //    this.axios.post(
    //   "http://localhost:3000/Login",
    //   {
    //     username: "daniel",
    //     password: "123456"
    //   }
      
    // ).then( res => {
    //   console.log(res);
      this.axios.get(
          "http://localhost:3000/users/favoriteGames",
        ).then(response => {
          console.log(response);
        let future_games_count = response.data.length;
        if (future_games_count > 3)
            future_games_count = 3;
        
        for(let i=0; i < future_games_count; i++){

          // let home_team_details = await this.axios.get(
          // `http://localhost:3000/teams/teamFullDetails/${response.data[i].home_team_id}`,
          // );
          // let guest_team_details = await this.axios.get(
          // `http://localhost:3000/teams/teamFullDetails/${response.data[i].guest_team_id}`,
          // );
          // console.log(home_team_details.data.team_name);
          // console.log(response.data[i].gamedetails[0].gameid);
          let game_details = {
          date_time: response.data[i].game_date_time,
       //   hour: response.data[i].date_time.slice(11,19),
          // home_team_name: home_team_details.data.team_name,
          // home_team_logo: home_team_details.data.logo,
          // guest_team_name: guest_team_details.data.team_name,
          // guest_team_logo: guest_team_details.data.logo,
          //field: response.data[i].field
          home_team_name: response.data[i].home_team_id,
          guest_team_name: response.data[i].guest_team_id

          };
          this.games.push(game_details);
          console.log(game_details);
        }
        })
      .catch( error =>{
        console.log("error in update games");
        console.log(error);
      });
        
    }
  },
    mounted(){
    console.log("Favorite games mounted")
    
  }  
};
</script>

<style></style>
