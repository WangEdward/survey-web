<script setup>
import Options from "./Options.vue";
</script>

<script>
export default {
  name: "Card",
  components: {
    Options,
  },
  props: {
    qid: {
      type: String,
      required: true,
    },
    qindex: {
      type: Number,
      required: true,
    },
    qtotal: {
      type: Number,
      required: true,
    },
  },
  emits: ["qscore"],
  data() {
    return {
      question: null,
      qscore: 0,
    };
  },
  methods: {
    async fetchCard() {
      this.question = null;
      const response = await fetch(
        `http://localhost:8080/mcq/byid/${this.qid}`
      );
      this.question = await response.json();
      console.log(this.question);
    },
  },
  mounted() {
    this.fetchCard();
  },
  watch: {
    qid: {
      handler() {
        this.fetchCard();
      },
    },
    qscore: {
      handler() {
        console.log(this.qscore);
        this.$emit("qscore", this.qscore);
      },
    },
  },
};
</script>

<template>
  <div class="card">
    <h3>Question {{ qindex + 1 }} / {{ qtotal }}</h3>
    <h1 v-if="!question">Loading...</h1>
    <div class="question" v-if="question">
      <h2>{{ question.questionDetail }}</h2>
      <Options
        :options="question.options"
        @option-score="(n) => (qscore = n)"
      />
    </div>
    <!-- <pre e>{{ question.questionDetail }}</pre>
    <Selections  :options="question.options" /> -->
  </div>
</template>
