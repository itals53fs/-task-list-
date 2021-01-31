<template>
  <div class="list">
    <div
      v-for="(tarefa, i) in tarefas"
      :key="tarefa.name"
      @click="status(i)"
      :class="{verde: !tarefa.requere}"
    >
      {{ tarefa.name }}
      <button @click.stop="deleteList(i)">x</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    tarefas: Array,
  },
  data() {
    return {
      index: "",
      verde: false,
    };
  },
  methods: {
    deleteList(i) {
      this.$emit("deleteList", i);
    },
    status(i) {
      this.$emit("status", i);
    },
  },
};
</script>

<style>

.list {
  margin: 10px;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  user-select: none;
  justify-content: center;
  width: 91%;
}
.list button {
  right: 0;
  margin-top: -60px;
  color: white;
  border: none;
  font-size: 1rem;
  font-weight: 900;
  position: absolute;
  border-radius: 2px;
  background: none;
}
.verde {
  text-decoration: line-through;
}
.list div {
  width: 100%;
  margin: 10px;
  max-width: 700px;
  text-align: center;
  display: flex;
  flex-direction: column;
  position: relative;
  height: 80px;
  justify-content: center;
  background: none;
  font-size: 20px;
  user-select: none;
  cursor: pointer;
  border: solid 1px rgb(85, 84, 84);
  border-left:none ;
  border-right:none ;
  border-radius: 10px;
}
</style>