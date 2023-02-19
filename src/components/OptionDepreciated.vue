<script>
// export class Option {
//   constructor(optionDetail, score, isCorrect) {
//     this.optionDetail = optionDetail;
//     this.score = score;
//     this.isCorrect = isCorrect;
//   }
// }
export default {
  name: "Option",
  props: {
    option: {
      type: Object,
      required: true,
    },
  },
  methods: {
    checkAnswer() {},
  },
};
</script>

<template>
  <div class="option">
    <input type="radio" :id="option.optionDetail" :name="option.optionDetail" />
    <label :for="option.optionDetail">{{ option.optionDetail }}</label>
  </div>
</template>
