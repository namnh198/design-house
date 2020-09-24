<template>
  <section class="authentication">
    <div class="auth-body">
      <h1 class="text-uppercase fw-500 mb-4 text-center font-22">
        Resend Verification Email
      </h1>
      <form class="auth-form" @submit.prevent="submit">
        <alert-error v-if="form.errors.has('message')" :form="form">
          {{ form.errors.get('message') }}
        </alert-error>
        <alert-success :form="form">
          We have resent the verification email
        </alert-success>
        <div class="form-group">
          <base-input
            :form="form"
            field="email"
            v-model="form.email"
            placeholder="Email"
          ></base-input>
        </div>

        <div class="text-right">
          <base-button :loading="form.busy">
            Resend
          </base-button>
        </div>
      </form>
    </div>
  </section>
</template>

<script>
export default {
  middleware: ['guest'],
  data() {
    return {
      form: this.$vform({
        email: ''
      })
    };
  },

  methods: {
    submit() {
      this.form
        .post(`/verification/resend`)
        .then(res => this.form.reset())
        .catch(e => console.log(e));
    }
  }
};
</script>

<style></style>
