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
    <div
      class="score-percentage"
      :style="{ 'margin-left': scorePercentage + '%' }"
    />
  </div>
  <div class="result">
    <p v-if="currentScore < 45">Within Normal Range</p>
    <p v-if="currentScore <= 59">Minimal to moderate anxiety</p>
    <p v-if="currentScore <= 74">Marked to severe anxiety</p>
    <p v-if="currentScore > 74">Most extreme anxiety</p>
    <p v-if="currentScore > 59">We suggest that you need to visit a psychologist.</p>
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
