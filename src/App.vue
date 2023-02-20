<script setup>
import Card from "./components/Card.vue";
</script>
<script>
export default {
  name: "App",
  components: {
    Card,
  },
  data() {
    return {
      qindex: 0,
      qlist: null,
      qtotal: 20,
      cardScore: 0,
      totalScore: 0,
      isDisabled: true,
    };
  },
  methods: {
    async fetchQuestions() {
      this.qlist = null;
      const response = await fetch(`http://localhost:8080/mcq/all_mcq_ids`);
      this.qlist = await response.json();
      console.log(this.qlist);
      this.qtotal = this.qlist.length;
      console.log(this.qtotal);
    },
    nextCard() {
      this.totalScore += this.cardScore;
      console.log("total score:" + this.totalScore);
      this.qindex++;
      this.isDisabled = true;
    },
  },
  watch: {
    // check score
  },
  mounted() {
    this.fetchQuestions();
  },
  computed: {
    progress() {
      return (this.qindex / this.qtotal) * 100;
    },
  },
};
</script>

<template>
  <!-- <header>
  </header> -->

  <main>
    <h3 v-if="!qlist">Loading...</h3>
    <h3 v-if="qlist && qindex >= qtotal">You have completed the quiz!</h3>
    <h3 v-if="qlist && qindex >= qtotal">Your total score is {{ totalScore }}</h3>
    <div class="qcontainer" v-if="qlist&& qindex < qtotal">
      <Card
        :qtotal="qtotal"
        :qindex="qindex"
        :qid="qlist[qindex]"
        @qscore="(n) => (cardScore = n) && (isDisabled = false)"
      ></Card>
      <button @click="nextCard" :disabled="isDisabled">
        <span class="text">next </span>
        <span class="arrow">&rarr;</span>
      </button>
    </div>
  </main>
  <div class="progress-bar" >
    <div class="progress-bar__fill" :style="{ width: progress + '%' }"></div>
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }
}
</style>
