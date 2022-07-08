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
<style scoped src="@/assets/css/style.css"></style>
