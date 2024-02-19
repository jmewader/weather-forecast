<script lang="ts">
import axios, { AxiosResponse } from "axios";

import { defineComponent } from "vue";

export default defineComponent({
  data() {
    return {
      city: "",
      error: "",
      info: null as AxiosResponse<any, any> | null,
    };
  },
  computed: {
    cityName(this: { city: string }) {
      return this.city;
    },
    showTemp(this: { info: any }) {
      return "Температура: " + this.info?.data?.main?.temp;
    },
    showFeelsLike(this: { info: any }) {
      return "Ощущается как: " + this.info?.data?.main?.feels_like;
    },
    showMinTemp(this: { info: any }) {
      return "Минимальная температура: " + this.info?.data?.main?.temp_min;
    },
    showMaxTemp(this: { info: any }) {
      return "Максимальная температура: " + this.info?.data?.main?.temp_max;
    },
  },
  methods: {
    getWeather() {
      if (this.city.trim().length < 2) {
        this.error = "Введите название больше двух символов";
        return false;
      }

      this.error = "";

      axios
        .get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=4ac85ff83534b44db19f8d1c08ec4fcf`)
        .then((res: AxiosResponse<any, any>) => {
          this.info = res;
          console.log("info", this.info.data.main.temp);
        })
        .catch((error: any) => {
          console.error("Error fetching weather data:", error);
        });
    },
  },
});
</script>

<template>
  <div class="container">
    <div class="block">
      <h1 class="block__title">Прогноз погоды~</h1>
      <p class="block__description">Узнай погоду в {{ city == "" ? "вашем городе" : cityName }}</p>

      <div class="block__action">
        <input v-model="city" class="block__input" type="text" placeholder="Введите город" />
        <button @click="getWeather()" v-if="city != ''" class="block__btn">Узнать погоду</button>
        <button disabled v-else class="block__btn">Узнать погоду</button>
      </div>
      <p class="block__error-text">{{ this.error }}</p>

      <div v-show="info != null">
        <p>{{ showTemp }}</p>
        <p>{{ showFeelsLike }}</p>
        <p>{{ showMinTemp }}</p>
        <p>{{ showMaxTemp }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  max-width: 1280px;
  height: 100vh;
  margin: 0 auto;
}

.block {
  width: 100%;
  max-width: 900px;
  min-height: 400px;
  border-radius: 30px;
  padding: 50px 20px;
  background-color: #070d0e;
  color: white;
  text-align: center;
  display: flex;
  flex-direction: column;
}

.block__title {
  font-size: 36px;
  margin: 0 0 16px;
}

.block__description {
  font-size: 18px;
}

.block__action {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  margin: 40px 0 0;
}

.block__input {
  background-color: transparent;
  border: 2px solid rgba(110, 110, 110, 0.322);
  border-radius: 6px;
  outline: none;
  min-height: 40px;
  padding: 0 10px;
  color: white;
}

.block__btn {
  background-color: #ffae00;
  min-height: 40px;
  min-width: 150px;
  padding: 0 20px;
  border: none;
  border-radius: 6px;
  color: white;
  font-weight: 500;
  cursor: pointer;
  transition: 0.25s;
  font-size: 16px;
  font-weight: 500;
}

.block__btn:disabled {
  background-color: gray;
  cursor: not-allowed;
}

:not(:disabled).block__btn:hover {
  background-color: rgb(0, 0, 0);
}

.block__error-text {
  color: rgb(168, 0, 0);
}
</style>
