<template>
  <section class="authentication">
    <div class="auth-body">
      <h1 class="text-uppercase fw-500 mb-4 text-center font-22">
        Resend Verification Email
      </h1>
      <form class="auth-form" @submit.prevent="submit">
        <div class="alert alert-danger" v-if="form.errors.has('message')" :form="form">
          {{ form.errors.get('message') }}
        </div>
        <div v-if="alert" class="alert alert-success">
          {{ alert }}
        </div>
        <div class="form-group">
          <input
                class="form-control form-control-lg font-14 fw-300"
                :class="{'is-invalid':form.errors.has('email')}"
                type="text"
                name="email"
                v-model="form.email"
                placeholder="Email"
            />
            <div class="alert alert-danger text-muted text-sm" v-if="form.errors.has('email')" v-html="form.errors.get('email')" />
        </div>

        <div class="text-right">
          <button type="submit" :disabled="form.busy"
            class="btn btn-primary primary-bg-color font-16 fw-500 text-up">
            <span v-if="form.busy">
              <i class="fas fa-spinner fa-spin"></i>
            </span>
            Resend
          </button>
        </div>
      </form>
    </div>
  </section>
</template>

<script>
export default {
  middleware:['guest'],
  data() {
    return {
      form: this.$vform({
        email: ''
      }),
      alert:null
    };
  },
  methods: {
    submit() {
      let self=this;
      this.form
        .post(`/verification/resend`)
        .then(res => {
          console.log(res);
          if(res.status==200){
            self.alert="We have resent the verification email";
            this.form.reset();
          }
          
        })
        .catch(e => console.log(e));
    }
  }
};
</script>