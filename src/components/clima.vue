<template>
  <div>
    <div class="result">
      <progress v-if="!clima"  class="carregando"/>
      <div v-else class="result">
        <h1>{{ clima }}</h1>
        <img :src="img" alt="" />
      </div>
    </div>
    <div class="input-clima">
      <input
        type="text"
        placeholder="Digite sua cidade..."
        v-model="cidade"
        @keyup.enter="climas"
      />
      <button @click="climas">&#10147;</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cidade: "Serro",
      clima: false,
      img: "",
    };
  },
  methods: {
    climas() {
      this.clima = false;
      let ajax = new XMLHttpRequest();
      ajax.open(
        "GET",
        `http://api.openweathermap.org/data/2.5/weather?q=${this.cidade}&appid==pt`
      );
      ajax.send();
      ajax.addEventListener("readystatechange", this.ready, false);
    },
    ready(event) {
      let ajax = event.target;
      if (ajax.status === 200 && ajax.readyState === 4) {
        let data = JSON.parse(ajax.responseText);
        this.img = `http://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`;
        this.clima = `${data.name} - ${data.main.temp}° ${data.weather[0].description}`;
      } else {
        this.clima = "Cidade Inválida";
      }
    },
  },
  created() {
    this.climas();
  },
};
</script>

<style>
* {
  font-family: "Lato", sans-serif;
}
.input-clima input {
  outline: none;
  color: white;
  font-weight: bold;
  font-size: 18px;
  background: none;
  border: none;
  border-bottom: solid 1px #ccc;
  padding: 10px;
  font-family: cursive;
}
.input-clima button {
  background: none;
  border: none;
  font-size: 30px;
  color: #ccc;
}
.result {
  display: flex;
  font-size: 40px;
}
.input-clima {
  display: flex;
  justify-content: center;
  margin: 40px 0 0 40px;
}
.carregando{
    width: 150px;
    height: 10px;
    margin: 0 auto;
}

</style>