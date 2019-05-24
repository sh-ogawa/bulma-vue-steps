<template>
  <div class="step-content has-text-centered is-active">
    <slot :step-index="stepIndex" />
  </div>
</template>
<script>
export default {
  name: 'StepItem',
  props: {
    label: {
      type: String,
      default: '',
    },
  },
  data() {
    return {
      stepIndex: 0,
    };
  },
  created() {
    this.$parent.stepItems.push(this);
    this.stepIndex = this.$parent.stepItems.length - 1;
  },
};
</script>

<style scoped>

</style>
