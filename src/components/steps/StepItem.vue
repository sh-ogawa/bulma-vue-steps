<template>
  <div class="step-content has-text-centered" :class="'is-active'">
    hoge
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
  created() {
    this.$parent.stepItems.push(this);
  },
};
</script>

<style scoped>

</style>
