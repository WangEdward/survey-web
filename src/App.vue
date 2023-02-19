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
    };
  },
  methods: {
    async fetchQuestions() {
      this.qlist = null;
      const response = await fetch(`http://localhost:8080/mcq/all_mcq_ids`);
      this.qlist = await response.json();
      console.log(this.qlist);
    },
    nextCard() {
      this.qindex++;
    },
  },
  watch: {
    // check score
  },
  mounted() {
    this.fetchQuestions();
  },
};
</script>

<template>
  <!-- <header>
  </header> -->

  <main>
    <h3 v-if="!qlist">Loading...</h3>
    <div class="qcontainer" v-if="qlist">
      <Card :qindex="qindex" :qid="qlist[qindex]"></Card>
      <button @click="nextCard">
        <span class="text">next </span>
        <span class="arrow">&rarr;</span>
      </button>
    </div>
  </main>
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

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
