<template>
<v-container>
  <h1>Weer rest van de week</h1>
   <v-row>

    </v-row>
</v-container>
   
</template>
<script>
export default {
  props:['weekForcast'],
  name: "WeatherHighlights",
  data() {
    return {
    };
  },
  mounted(){
    console.log("Week forcast: ",this.weekForcast)
  }
};
</script>
<style scoped>
* {
    font-family: "Roboto" !important; 
    color: white !important;
    margin: 0 !important;
  }
  .Card{
    justify-content: center !important;
    text-align: center !important;
    background-color: #18212D !important;
    border-radius: 2em !important;
  }
  .leftCard{
    border-radius: 0px !important 
  }
  .cardTitle{
    justify-content: center !important;
  }
  .cardText{
    font-size:large;
  }
    .img{
  left: 50%;
  transform: translate( -50%);
  }
</style>
