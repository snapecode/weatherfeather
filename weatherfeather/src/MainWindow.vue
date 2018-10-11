<template>
  <Window title="The Weather Feather" width="400" height="200" margined v-on:close="exit">
    <Box padded>
      <Text>Lets see the weather somewhere, we hope it's light as a feather!!</Text>
      <Box horizontal padded>
        <TextInput stretchy v-model="query"/>
        <Button :enabled="!!query" @click="showWeather">Lets have a look then, shall we??</Button>
      </Box>
      <Separator horizontal/>
      <Group margined>
        <Box padded>
          <Text v-if="error">Sorry, we don't have any weather data for that place.</Text>
          <Box v-if="!!city">
            <Box padded horizontal>
              <Text stretchy>{{city}}, {{country}}</Text>
              <Text>{{temp}}&deg;C</Text>
            </Box>
            <Text>{{weatherDescription}}</Text>
            <Seperator horizontal/>
            <Box padded horizontal>
              <Text stretchy>Min:{{tempMin}}&deg;C</Text>
              <Text stretchy>Max:{{tempMax}}&deg;C</Text>
              <Text stretchy>Humidity:{{humidity}}%</Text>
            </Box>
          </Box>
        </Box>
      </Group>
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
      axios.get(
        `/weather?q=${
          this.query
        }&units=metric&&appid=97be0bd3696bb8db65b88f3edcd0dc78`,
      )
        .then(response =>{
          this.city = response.data.name;
          this.country = response.data.sys.country;
          this.weatherDescription = response.data.weather[0].description;
          this.temp = response.data.main.temp;
          this.tempMin = response.data.main.temp_min;
          this.tempMax = response.data.main.temp_max;
          this.humidity = response.data.main.humidity;
          this.error = false;
      })
      .catch(() =>{
      this.error = true;
      this.city = '';
    });
  },
},
};

</script>
