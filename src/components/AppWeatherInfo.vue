<script>
export default {
  props: ['weatherData'],

  data() {
    return {}
  },
}
</script>

<template>
  <div class="info">
    <h2 class="info-city">{{ weatherData.city }}, {{ weatherData.country }}</h2>

    <img class="info-img" :src="`./src/assets/${weatherData.condition.toLowerCase()}.png`" />

    <div class="info-main">
      <p class="info-main-temperature">{{ weatherData.temperature }}&#176;C</p>
      <p class="info-main-condition">{{ weatherData.detailedCondition }}</p>
    </div>

    <p class="info-humidity">
      <font-awesome-icon class="info-humidity-icon" icon="fa-solid fa-water" />
      <span class="info-humidity-value">{{ weatherData.humidity }}%</span>
      <span class="info-humidity-header">Humidity</span>
    </p>

    <p class="info-wind">
      <font-awesome-icon class="info-wind-icon" icon="fa-solid fa-wind" />
      <span class="info-wind-value">{{ weatherData.wind }}km/h</span>
      <span class="info-wind-header">Wind speed</span>
    </p>

    <p class="info-pressure">
      <font-awesome-icon class="info-pressure-icon" icon="fa-solid fa-thermometer-half" />
      <span class="info-pressure-value">{{ weatherData.pressure }}mb</span>
      <span class="info-pressure-header">Pressure</span>
    </p>
  </div>
</template>

<style lang="scss">
.info {
  display: grid;
  grid-template-rows: repeat(4, auto);
  grid-template-columns: repeat(3, 1fr);
  justify-items: center;
  gap: 30px 50px;
  overflow: hidden;

  &-city {
    grid-area: 1/1/2/4;
    margin-top: 40px;
    font-size: 3em;
  }

  &-img {
    grid-area: 2/1/3/4;
  }

  &-main {
    grid-area: 3/1/4/4;
    font-size: 2em;
    text-align: center;
    margin-bottom: 50px;

    &-temperature {
      font-size: 2em;
      font-weight: 700;
    }
  }

  &-humidity,
  &-wind,
  &-pressure {
    display: grid;
    grid-template-columns: repeat(2, auto);
    grid-template-rows: repeat(2, min-content);
    gap: 0 20px;

    &-icon {
      grid-area: 1/1/3/2;
      align-self: center;
      font-size: 2.5em;
    }

    &-value {
      font-size: 1.5em;
    }

    &-header {
      font-size: 1em;
    }
  }
}
</style>