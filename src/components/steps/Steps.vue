<template>
  <section>
    <div class="steps">
      <div v-for="(stepItem, index) in stepItems" :key="index"
           class="step-item" :class="newStep === index ? 'is-active' : ''"
      >
        <div class="step-marker">{{ index + 1 }}</div>
        <div class="step-details">
          <p class="step-title">{{ stepItem.label }}</p>
        </div>
      </div>
      <section class="steps-content">
        <slot />
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
      // Stepが追加してくる
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
      if (this.newStep < this.stepItems.length - 1) {
        this.newStep += 1;
      }
    },
  },
  watch: {
    stepItems: {
      // deep watchしてないから初回の一発目だけ呼ばれる
      // ちなみにdeep watchして中のフラグ書き換えると無限ループするから、やったらダメ
      handler() {
        this.stepItems.forEach((item, index) => {
          if (this.newStep === index) {
            item.activate();
          } else {
            item.deactivate();
          }
        });
      },
    },
    newStep(value) {
      this.stepItems.forEach((item, index) => {
        if (value === index) {
          item.activate();
        } else {
          item.deactivate();
        }
      });
      this.$emit('input', value);
    },
  },
};
</script>

<style scoped>
</style>
