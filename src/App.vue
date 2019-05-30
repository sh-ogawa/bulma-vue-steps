<template>
    <section>
      <steps
        v-model="newStep"
        :first-step-previous-handler="firstPreviousAction"
        :last-step-next-handler="lastNextAction"
        :disabled-previous-action="disabledAction"
        :disabled-next-action="disabledAction"
      >
        <step-item :label="'test1'">
          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">Username</label>
            </div>
            <div class="field-body">
              <div class="field">
                <div class="control">
                  <input class="input"
                         name="username"
                         id="username"
                         type="text"
                         placeholder="Username"
                         autofocus data-validate="require">
                </div>
              </div>
            </div>
          </div>
        </step-item>
        <step-item :label="'test2'">
          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">Password</label>
            </div>
            <div class="field-body">
              <div class="field">
                <div class="control has-icon has-icon-right">
                  <input class="input"
                         type="password"
                         name="password"
                         id="password"
                         placeholder="Password"
                         data-validate="require">
                </div>
              </div>
            </div>
          </div>
        </step-item>
      </steps>
    </section>
</template>

<script>
import Steps from '@/components/steps/Steps';
import StepItem from '@/components/steps/StepItem';

// Example of how to use step component
export default {
  name: 'App',
  components: { StepItem, Steps },
  data() {
    return {
      newStep: 0,
    };
  },
  computed: {
    disabledAction() {
      return false;
    },
  },
  methods: {
    firstPreviousAction() {
      alert('click previous button at first step');
    },
    lastNextAction() {
      alert('click next button at last step');
    },
  },
};
</script>

<style lang="sass">
  @import "~bulma/bulma.sass"
  @import "~bulma-steps/dist/css/bulma-steps"
</style>
