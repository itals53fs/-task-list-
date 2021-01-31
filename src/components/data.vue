<template>
  <div class="data">
    <input
      type="text"
      placeholder="Nova tarefa?"
      @keyup.enter="add"
      v-model="name"
    />
    <button @click="add">+</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "",
    };
  },
  methods: {
    add() {
      this.$emit("addList", { name: this.name, requere: true });
      this.name = "";
    },
  },
};
</script>

<style>
.data input {
  outline: none;
  border: solid 1px #ccc;
  background: none;
  border-radius: 5px 0px 0px 5px;
  border-right: none;
  padding: 10px;
  width: 40%;
  color: white;
  font-weight: 600;
  font-size: 16px;
  user-select: none;
}
.data {
  width: 100%;
  text-align: center;
}
.data button {
  font-weight: 600;
  font-size: 16px;
  outline: none;
  border: solid 1px #ccc;
  background-color: teal;
  border-radius: 0px 5px 5px 0px;
  border-left: none;
  color: white;
  font-weight: 900;
  height: 41px;
}
@media(max-width:400px){
    .data input{
        width: 80%;
    }
}
</style>