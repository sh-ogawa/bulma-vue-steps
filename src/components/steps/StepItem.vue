<template>
  <div v-show="isActive">
    <div class="step-content has-text-centered is-active">
      <slot />
    </div>
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
      isActive: false,
    };
  },
  created() {
    this.$parent.stepItems.push(this);
  },
  methods: {
    activate() {
      this.isActive = true;
    },

    /**
     * Deactivate tab, alter animation name based on the index.
     */
    deactivate() {
      this.isActive = false;
    },
  },
};
</script>

<style scoped>

</style>
