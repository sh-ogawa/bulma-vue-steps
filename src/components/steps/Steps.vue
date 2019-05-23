<template>
  <section>
    <div class="steps" id="stepsDemo">
      <div class="step-item" :class="passFirstStep">
        <div class="step-marker">1</div>
        <div class="step-details">
          <p class="step-title">Account</p>
        </div>
      </div>
      <div class="step-item" :class="passSecondStep">
        <div class="step-marker">2</div>
        <div class="step-details">
          <p class="step-title">Profile</p>
        </div>
      </div>
      <div class="step-item" :class="passThirdStep">
        <div class="step-marker">3</div>
        <div class="step-details">
          <p class="step-title">Social</p>
        </div>
      </div>
      <div class="step-item" :class="passLastStep">
        <div class="step-marker">4</div>
        <div class="step-details">
          <p class="step-title">Finish</p>
        </div>
      </div>
      <div class="steps-content">
        <div class="step-content has-text-centered" :class="isFirstStep">
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
          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">Confirm password</label>
            </div>
            <div class="field-body">
              <div class="field">
                <div class="control has-icon has-icon-right">
                  <input class="input"
                         type="password"
                         name="password_confirm"
                         id="password_confirm"
                         placeholder="Confirm password"
                         data-validate="require">
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="step-content has-text-centered" :class="isSecondStep">
          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">Firstname</label>
            </div>
            <div class="field-body">
              <div class="field">
                <div class="control">
                  <input class="input"
                         name="firstname"
                         id="firstname"
                         type="text"
                         placeholder="Firstname"
                         autofocus data-validate="require">
                </div>
              </div>
            </div>
          </div>
          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">Last name</label>
            </div>
            <div class="field-body">
              <div class="field">
                <div class="control has-icon has-icon-right">
                  <input class="input"
                         type="text"
                         name="lastname"
                         id="lastname"
                         placeholder="Last name"
                         data-validate="require">
                </div>
              </div>
            </div>
          </div>
          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">Email</label>
            </div>
            <div class="field-body">
              <div class="field">
                <div class="control has-icon has-icon-right">
                  <input class="input"
                         type="email"
                         name="email"
                         id="email"
                         placeholder="Email"
                         data-validate="require">
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="step-content has-text-centered" :class="isThirdStep">
          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">Facebook account</label>
            </div>
            <div class="field-body">
              <div class="field">
                <div class="control">
                  <input class="input"
                         name="facebook"
                         id="facebook"
                         type="text"
                         placeholder="Facebook account url"
                         autofocus data-validate="require">
                </div>
              </div>
            </div>
          </div>
          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">Twitter account</label>
            </div>
            <div class="field-body">
              <div class="field">
                <div class="control">
                  <input class="input"
                         name="twitter"
                         id="twitter"
                         type="text"
                         placeholder="Twitter account url"
                         autofocus data-validate="require">
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="step-content has-text-centered" :class="isLastStep">
          <h1 class="title is-4">Your account is now created!</h1>
        </div>
      </div>
      <div class="steps-actions">
        <div class="steps-action">
          <a href="#" data-nav="previous" class="button is-light" @click="previousStep">Previous</a>
        </div>
        <div class="steps-action">
          <a href="#" data-nav="next" class="button is-light" @click="nextStep">Next</a>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Steps',
  data() {
    return {
      newStep: 1,
    };
  },
  // passHogeが名前がアレになってしまったので直す
  // 入力中か通過済を表すやつ
  computed: {
    isFirstStep() {
      return this.newStep === 1 ? 'is-active' : '';
    },
    passFirstStep() {
      return this.newStep >= 1 ? 'is-active is-success' : '';
    },
    isSecondStep() {
      return this.newStep === 2 ? 'is-active' : '';
    },
    passSecondStep() {
      return this.newStep >= 2 ? 'is-active is-success' : '';
    },
    isThirdStep() {
      return this.newStep === 3 ? 'is-active' : '';
    },
    passThirdStep() {
      return this.newStep >= 3 ? 'is-active is-success' : '';
    },
    isLastStep() {
      return this.newStep === 4 ? 'is-active' : '';
    },
    passLastStep() {
      return this.newStep >= 4 ? 'is-active is-success' : '';
    },
  },
  methods: {
    previousStep() {
      if (this.newStep > 1) {
        this.newStep -= 1;
      }
    },
    nextStep() {
      if (this.newStep < 4) {
        this.newStep += 1;
      }
    },
  },
};
</script>

<style lang="sass" scoped>
@import "~bulma/bulma.sass"
@import "~bulma-steps/dist/css/bulma-steps"
</style>
