<script>
import axios from 'axios';
import AppWeatherInfo from './components/AppWeatherInfo.vue';
import AppNotFound from './components/AppNotFound.vue';

export default {
  components: { AppWeatherInfo, AppNotFound },

  data() {
    return {
      URL: 'https://api.openweathermap.org/data/2.5/weather',
      API: 'a9364650d7bb1a7f29a975686cbc4543',
      location: '',
      weatherData: {},
      success: false,
      error: false,
    }
  },

  methods: {
    getForecast() {
      this.success = false;
      this.error = false;

      axios.get(this.URL + '?q=' + this.location + '&appid=' + this.API + '&units=metric')
        .then(res => {
          if (res.status === 200) {
            this.error = false
            this.success = true;

            this.weatherData = {
              city: res.data.name,
              country: res.data.sys.country,
              temperature: Math.round(res.data.main.temp),
              humidity: res.data.main.humidity,
              wind: res.data.wind.speed,
              condition: res.data.weather[0].main,
              detailedCondition: res.data.weather[0].description.toUpperCase(),
              pressure: res.data.main.pressure,
            }

            console.log(res);
          }
        })
        .catch(err => {
          console.log(err);
          this.success = false;
          this.error = true;
        })
    },
  },
}
</script>

<template>
  <div class="container">
    <div class="search">
      <font-awesome-icon icon="fa-solid fa-location-dot" />
      <input class="search-input" type="text" v-model="location" placeholder="Enter location" />
      <font-awesome-icon icon="fa-solid fa-magnifying-glass" class="search-btn" @click="getForecast" />
    </div>

    <Transition name="show" mode="out-in">
      <AppWeatherInfo v-if="success" :weatherData="weatherData"></AppWeatherInfo>
    </Transition>
    <Transition name="show" mode="out-in">
      <AppNotFound v-if="error"></AppNotFound>
    </Transition>
  </div>
</template>

<style lang="scss">
.container {
  border-radius: 20px;
  padding: 50px;
  background-color: #ffffff;
  box-shadow: 0 0 50px #ffffff;
}

.search {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
  border: 2px solid #000000;
  border-radius: 20px;
  padding: 10px 30px;
  font-size: 2em;

  &-input {
    height: 50px;
    border: none;
    outline: none;
    text-align: center;
    font-size: 1em;
    text-transform: uppercase;

    &::placeholder {
      font-size: 1em;
    }
  }

  &-btn {
    transition: 0.3s;
    cursor: pointer;

    &:hover {
      transform: scale(1.1);
    }
  }
}

.show-enter-from,
.show-leave-to {
  opacity: 0;
}

.show-enter-active {
  transition: all 0.5s ease-in-out;
}
</style>