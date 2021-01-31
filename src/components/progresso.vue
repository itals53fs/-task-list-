<template>
    <div class="progrsso">
      <div :style="{width: `${porcento}%`}">
          <span>{{ porcento }}%</span>
          </div>
  </div>
</template>

<script>
export default {
  props: {
    porcento: Number
  },
  data() {
    return {};
  },
};
</script>
<style>
    .progrsso{
        width: 71%;
        border: solid 1px #CCC;
        text-align: center;
        border-radius: 10px;
        margin: 20px;
        position:relative;
        display: flex;
        justify-content: center;
    }
    .progrsso div{
        background-color:teal;
        border-radius: 10px;
        height: 20px;
    }
    .progrsso span{
        position: absolute;
        text-align: center;
    }
</style>