<template>
  <div class="player-full">
    <ul class="player-content">
      <li> Common name: {{ commonName }}</li>
      <li> Nationality: {{ nationality }}</li>
      <li> Birthdate: {{ birthdate }}</li>
      <li> Birth Country: {{ birthCountry }}</li>
      <li> Height: {{ height }}</li>
      <li> Weight: {{ weight }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "PlayerFullDetails",
  props: {
      commonName: {
        type: String,
        required: true
      },
      nationality: {
        type: String,
        required: true
      },
      birthdate: {
        type: String,
        required: true
      },
      birthCountry: {
        type: String,
        required: true
      },
      height: {
        type: String,
        required: true
      },
      weight: {
        type: String,
        required: true
      }
  }, 
  mounted(){
    console.log("player full mounted")
  } 
};
</script>

<style>
.player-full {
  display: inline-block;
  width: 250px;
  height: 200px;
}

.player-full .player-title {
  text-align: center;
  text-transform: uppercase;
  color:  rgb(111, 197, 157);
}

.player-full .player-content {
  width: 100%;
  overflow: hidden;
}



</style>
