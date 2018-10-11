<template>
  <Window title="weatherfeather" width="400" height="100" margined v-on:close="exit">
    <Box padded>
      <Text>Lets see the weather, we hope it's light as a feather!!</Text>
      <Box horizontal padded>
        <TextInput v-model="query" stretchy></TextInput>
        <Button :enabled="!query">Lets have a look then, shall we??</Button>
      </Box>
    </Box>
  </Window>
</template>

<script>

  import axios from 'axios';
  axios.defaults.baseURL='http://api.openweathermap.org/data/2.5'
  const apiKey=process.env.API_KEY;


export default {
  data() {
    return {
      query: '',
      error: false,
      city: '',
      country: '',
      weatherDescription: '',
      temp: null,
      tempMin: null,
      tempMax: null,
      humidity: null,
    };
  },
methods:{
    exit(){
      this.$exit();
    },
  showWeather(){
      axios.get('/weather?q=${this.query}&units=metric&&appid=${apiKey}',)
        .then(response=>{
          this.city=response.data.name;
          this.country=response.data.name;
          this.weatherDescription=response.data.weather[0].description;
          this.temp=response.data.main.temp;
          this.tempMin=response.data.main.temp_min;
          this.tempMax=response.data.main.temp_max;
          this.humidity=response.data.main.humidity;
          this.error=false;
      })
    .catch(()=>{
      this.error=true;
      this.city='';
    });
  },
},
};

</script>
