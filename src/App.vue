<template>
  <div className="container">
    <div className="block">
      <h1 class="block__title">Прогноз погоды</h1>
      <p className="block__description">Узнай погоду в своем городе</p>

      <div className="block__action">
        <input className="block__input" type="text" placeholder="Введите город" />
        <button className="block__btn">Узнать погоду</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "App",
  // components: {
  //   HelloWorld
  // }
});
</script>

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
  background: transparent;
  border: 2px solid rgba(110, 110, 110, 0.322);
  border-radius: 6px;
  outline: none;
  min-height: 40px;
  padding: 0 10px;
  color: white;
}

.block__btn {
  background: #ffae00;
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

.block__btn:hover {
  background: rgb(0, 0, 0);
}
</style>
