<template>
    <section class="authentication">
    <div class="auth-body">
      <h1 class="text-uppercase fw-500 mb-4 text-center font-22">
        Login
      </h1>
      <div class="alert alert-danger text-muted text-sm" v-if="form.errors.has('message')"  >
        {{ form.errors.get('message') }}
          <nuxt-link :to="{name:'verification.resend'}">Resend verification email</nuxt-link>
      </div>
      <form class="auth-form" @submit.prevent="submit" >
        <div class="form-group">
            <base-input 
              :form="form"
              field="email"
              v-model="form.email"
              placeholder="Email"
            ></base-input>
           
        </div>
        <div class="form-group">
          <base-input 
              :form="form"
              field="password"
              inputType="password"
              v-model="form.password"
              placeholder="Password"
            ></base-input>
         
        </div>
        <div class="mt-4 mb-4 clearfix">
          <nuxt-link :to="{name:'password.email'}"
            
            class="forgot-pass color-blue font-14 fw-400"
          >
            Forgot password?
          </nuxt-link>
        </div>
        <div class="text-right">
          <base-button :loading="form.busy">Login</base-button>
          
        </div>
        <p class="font-14 fw-400 text-center mt-4">
          Don't have an account yet?
          <nuxt-link :to="{name:'register'}"  class="color-blue">
            Create an account
          </nuxt-link>
        </p>
      </form>
    </div>
  </section>
</template>
<script>


export default{
  middleware:['guest'],

  data(){
    return {
      form:this.$vform({
        email:"",
        password:"",
      }),
      alert:null
    }
  },
  methods:{
    submit(){
      this.$auth.loginWith('laravelJWT',{
        data:this.form
      })
      .then(res=>{
        console.log(res)
      })
      .catch(error=>{
        console.log(error.response.data.errors);
        this.form.errors.set(error.response.data.errors);
      });
    }
  }
}
</script>