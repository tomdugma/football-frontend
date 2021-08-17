<template>
  <div class="player-preview">
    <div :title="id" class="player-title">
      <b> {{ fullname }}</b>
      <img width="100" height="150" :src="image">

    </div>
    <ul class="player-content">
      <li> Team name: {{ team_name }}</li>
      <li> Position: {{ position }}</li>

    </ul>
  </div>
</template>

<script>
export default {
  name: "PlayerPreview",
  props: {
      full_name: {
        type: String,
        required: true
      },
      team_name: {
        type: String,
        required: true
      },
      image: {
        type: String,
        required: true
      },
      position: {
        type: String,
        required: true
      }
  }, 
  mounted(){
    console.log("player preview mounted")
  } 
};
</script>

<style>
.player-preview {
  display: inline-block;
  width: 250px;
  height: 90px;
}

.player-preview .player-title {
  text-align: center;
  color:  rgb(111, 197, 157);
}

.player-preview .player-content {
  width: 100%;
  overflow: hidden;
}



</style>
