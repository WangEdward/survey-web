<script setup>
// import Option from "./Option.vue";
</script>
<script>
export default {
  name: "Options",
  data() {
    return {
      selectedOption: null,
    };
  },
  props: {
    options: {
      type: Array,
      required: true,
    },
  },
  emits: ["optionScore"],
  methods: {
    submitAnswer(option) {
      this.selectedOption = option.score;
      this.$emit("optionScore", this.selectedOption);
      // console.log(this.selectedOption);
    },
  },
};
</script>
<template>
  <div class="options">
    <label
      v-for="(option, index) in options"
      :key="index"
      class="option"
      @click="submitAnswer(option)"
    >
      <input type="radio" :value="option.score" v-model="selectedOption" />
      <span class="option-text">{{ option.optionDetail }}</span>
    </label>
    <!-- <Option v-for="(option, index) in options" :key="index" :option="option" /> -->
  </div>
</template>
