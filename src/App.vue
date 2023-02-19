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
      qid: "638c95c678624c7a42822ad6",
    };
  },
  watch: {
    // check score
  },
};
</script>

<template>
  <!-- <header>
    <img
      alt="Vue logo"
      class="logo"
      src="./assets/logo.svg"
      width="125"
      height="125"
    />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header> -->

  <main>
    <Card :qindex="qindex" :qid="qid"></Card>
    <button @click="qindex++">
      <span class="text">next </span>
      <span class="arrow">&rarr;</span>
    </button>
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
