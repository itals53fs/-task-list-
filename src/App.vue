<template>
  <div id="app">
    <clima />
    <h1>Tarefas</h1>
    <Progresso :porcento="porcento" />

    <Data @addList="add" />

    <List
      :tarefas="tarefas"
      @deleteList="tarefas.splice($event, 1)"
      @status="status"
    />
  </div>
</template>

<script>
import Clima from "./components/clima.vue";
import Data from "./components/data.vue";
import List from "./components/list.vue";
import Progresso from "./components/progresso.vue";

export default {
  components: { Progresso, Data, List, Clima },
  data() {
    return {
      tarefas: [],
    };
  },
  methods: {
    status(i) {
      this.tarefas[i].requere = !this.tarefas[i].requere;
    },
    add(eventValue) {
      const compareble = (t) => t.name == eventValue.name;
      const tarefa = this.tarefas.filter(compareble).length === 0;
      if (tarefa) {
        this.tarefas.push(eventValue);
      }
    },
  },
  computed: {
    ativos() {
      let ativo = 0;
      this.tarefas.forEach((element) => {
        if (!element.requere) ativo++;
      });
      return ativo;
    },
    total() {
      return this.tarefas.length;
    },
    porcento() {
      const done = this.tarefas.filter((t) => !t.requere).length;
      return parseFloat(((done * 100) / this.tarefas.length).toFixed(2)) || 0;
    },
  },
  watch: {
    addTarefa: {
      deep: true,
      handler() {
        localStorage.setItem("tarefa", JSON.stringify(this.tarefas));
      },
    },
  },
  created() {
    const json = localStorage.getItem("tarefa");
    const array = JSON.parse(json);
    this.tarefas = Array.isArray(array) ? array : [];
  },
};
</script>

<style>
body {
  font-family: "Lato", sans-serif;
  background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
  color: #fff;
}

#app {
  display: flex;
  flex: 1;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  align-items: center;
}

#app h1 {
  margin-bottom: 5px;
  font-weight: 300;
  font-size: 3rem;
  max-width: 800px;
}
#app input {
  font-family: "Lato", sans-serif;
}
@media (max-width: 500px) {
  #app h1 {
    font-size: 18px;

  }
  img{
    width: 50px;
    
  }
}
</style>
