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
                  :disabled="disabledPreviousAction"
                  @click="previousStep">{{ previousButtonText }}</button>
        </div>
        <div class="steps-action">
          <button type="button" class="button is-light"
                  :disabled="disabledNextAction"
                  @click="nextStep">{{ nextButtonText }}</button>
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
    disabledPreviousAction: {
      type: Boolean,
      default: false,
    },
    disabledNextAction: {
      type: Boolean,
      default: false,
    },
    firstStepPreviousHandler: {
      type: Function,
      required: true,
    },
    lastStepNextHandler: {
      type: Function,
      required: true,
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
    previousButtonText() {
      return this.newStep > 0 ? this.previousText : 'back';
    },
    nextButtonText() {
      return this.newStep < this.stepItems.length - 1 ? this.nextText : 'finish';
    },
  },
  methods: {
    async previousStep() {
      if (this.newStep > 0) {
        this.newStep -= 1;
      } else {
        await this.firstStepPreviousHandler();
      }
    },
    async nextStep() {
      if (this.newStep < this.stepItems.length - 1) {
        this.newStep += 1;
      } else {
        await this.lastStepNextHandler();
      }
    },
    switchSteps(value) {
      this.stepItems.forEach((item, index) => {
        if (value === index) {
          item.activate();
        } else {
          item.deactivate();
        }
      });
    },
  },
  watch: {
    stepItems: {
      // deep watchしてないから初回の一発目だけ呼ばれる
      // ちなみにdeep watchして中のフラグ書き換えると無限ループするから、やったらダメ
      handler() {
        this.switchSteps(this.newStep);
      },
    },
    newStep(value) {
      this.switchSteps(value);
      this.$emit('input', value);
    },
  },
};
</script>

<style scoped>
</style>
