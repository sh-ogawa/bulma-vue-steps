<template>
  <section>
    <div class="steps">
      <div v-for="(stepItem, index) in stepItems" :key="index"
           class="step-item" :class="newStep === index ? 'is-active' : ''"
      >
        <div class="step-marker">{{ index + 1 }}</div>
        <div class="step-details">
          <p class="step-title">{{ stepItem.lable }}</p>
        </div>
      </div>
      <section class="steps-content">
        <slot :is-active="newStep === 1" />
      </section>

      <div class="steps-actions">
        <div class="steps-action">
          <button type="button" class="button is-light"
                  @click="previousStep">{{ previousText }}</button>
        </div>
        <div class="steps-action">
          <button type="button" class="button is-light"
                  @click="nextStep">{{ nextText }}</button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import StepItem from './StepItem';

export default {
  name: 'Steps',
  components: { StepItem },
  props: {
    value: {
      type: Number,
      default: 0,
    },
    previousText: {
      type: String,
      default: 'Previous',
    },
    nextText: {
      type: String,
      default: 'Next',
    },
  },
  data() {
    return {
      newStep: this.value,
      stepItems: [],
    };
  },
  computed: {
  },
  methods: {
    previousStep() {
      if (this.newStep > 0) {
        this.newStep -= 1;
      }
    },
    nextStep() {
      if (this.newStep < this.stepItems.length) {
        this.newStep += 1;
      }
    },
  },
  watch: {
    newStep(value) {
      this.$emit('input', value);
    },
  },
};
</script>

<style scoped>
</style>
