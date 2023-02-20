<script setup>
// import Option from "./Option.vue";
</script>
<script>
export default {
  name: "ResultCard",
  props: {
    currentScore: {
      type: Number,
      required: true,
    },
    totalScore: {
      type: Number,
      required: true,
    },
  },
  computed: {
    scorePercentage() {
      console.log(this.currentScore / this.totalScore);
      return Math.round((this.currentScore / this.totalScore) * 100);
    },
  },
  mounted() {
    console.log(this.scorePercentage);
  },
};
</script>

<template>
  <div class="gradient">
    <div class="score-percentage" :style="{'margin-left': scorePercentage + '%' }" />
  </div>
</template>
<style>
.gradient {
  height: 10px;
  background-color: red;
  background-image: linear-gradient(to right, green 25%, red 75%);
}

.score-percentage {
  width: 3px;
  height: 100%;
  background-color: black;
}
</style>
