<template>
    <section class="authentication">
    <div class="auth-body">
      <h1 class="text-uppercase fw-500 mb-4 text-center font-22">
        Reset Password
      </h1>
      <div class="alert alert-danger text-muted text-sm" v-if="form.errors.has('message')"  >
        {{ form.errors.get('message') }}
      </div>
      <div v-if="alert" class="alert alert-success">
          {{ alert }}
      </div>
      <form class="auth-form" @submit.prevent="submit" >
        <div class="form-group">
            <input
                class="form-control form-control-lg font-14 fw-300"
                :class="{'is-invalid':form.errors.has('email')}"
                type="text"
                :readonly="true"
                name="email"
                v-model="form.email"
                placeholder="Email"
            />
        </div>
        <div class="form-group">
            <input
                class="form-control form-control-lg font-14 fw-300"
                :class="{'is-invalid':form.errors.has('password')}"
                type="password"
                name="password"
                v-model="form.password"
                placeholder="Password"
            />
        </div>
        <div class="alert alert-danger text-muted text-sm" v-if="form.errors.has('password')" v-html="form.errors.get('password')" />
        <div class="form-group">
            <input
                class="form-control form-control-lg font-14 fw-300"
                :class="{'is-invalid':form.errors.has('password_confirmation')}"
                type="password"
                name="password_confirmation"
                v-model="form.password_confirmation"
                placeholder="Password Confirmation"
            />
        </div>
        
          
        
        <div class="text-right">
          <button type="submit" :disabled="form.busy"
            class="btn btn-primary primary-bg-color font-16 fw-500 text-up">
            <span v-if="form.busy">
              <i class="fas fa-spinner fa-spin"></i>
            </span>
            Reset Password
          </button>
        </div>
        <p class="font-14 fw-400 text-center mt-4">
        
          <nuxt-link :to="{name:'login'}"  class="color-blue">
            back to Login
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
        password_confirmation:"",
        token:""
      }),
      alert:null
    }
  },
  methods:{
    submit(){
      this.form.post('/password/reset')
      .then(res=>{
          if(res.status==200){
              console.log(res)
              this.alert=res.data.status;
              this.form.reset();
          }
      }).catch(e=>{
          console.log(e)
      })
    }
  },
  created(){
      this.form.email=this.$route.query.email;
      this.form.token=this.$route.params.token;
  }
}
</script>