<template>
    <section class="authentication">
    <div class="auth-body">
      <h1 class="text-uppercase fw-500 mb-4 text-center font-22">Register</h1>
      <div v-if="alert" class="alert alert-success">{{ alert }}</div>
      <form class="auth-form" @submit.prevent="submit">
       
        <div class="form-group">
          <input
                class="form-control form-control-lg font-14 fw-300"
                :class="{'is-invalid':form.errors.has('name')}"
                type="text"
                name="name"
                v-model.trim="form.name"
                placeholder="Full Name"
            />
            <div class="alert alert-danger text-muted text-sm" v-if="form.errors.has('name')" v-html="form.errors.get('name')" />
        </div>
        <div class="form-group">
            <input
                class="form-control form-control-lg font-14 fw-300"
                type="text"
                name="username"
                :class="{'is-invalid':form.errors.has('username')}"
                v-model.trim="form.username"
                placeholder="User Name"
            />
            <div class="alert alert-danger text-muted text-sm" v-if="form.errors.has('username')" v-html="form.errors.get('username')" />
          
        </div>
        <div class="form-group">
          <input
                class="form-control form-control-lg font-14 fw-300"
                :class="{'is-invalid':form.errors.has('email')}"
                type="email"
                name="email"
                v-model.trim="form.email"
                placeholder="Email"
          />
          <div class="alert alert-danger text-muted text-sm" v-if="form.errors.has('email')" v-html="form.errors.get('email')" />
        </div>
        <div class="form-group">
          <input
                class="form-control form-control-lg font-14 fw-300"
                :class="{'is-invalid':form.errors.has('password')}"
                type="password"
                name="password"
                v-model.trim="form.password"
                placeholder="Password"
          />
          <div class="alert alert-danger text-muted text-sm" v-if="form.errors.has('password')" v-html="form.errors.get('password')" />
        </div>
        <div class="form-group">
            <input
                class="form-control form-control-lg font-14 fw-300"
                type="password"
                name="password_confirmation"
                v-model.trim="form.password_confirmation"
                placeholder="Confirm Password"
          />
        
        </div>

        <div class="text-right">
          <button type="submit" :disabled="form.busy"
            class="btn btn-primary primary-bg-color font-16 fw-500 text-up">
            <span v-if="form.busy">
              <i class="fas fa-spinner fa-spin"></i>
            </span>
            Register
          </button>
        </div>
        <p class="font-14 fw-400 text-center mt-4">
          Already have an account?
          <nuxt-link :to="{name:'login'}" class="color-blue">Login</nuxt-link>
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
        username:"",
        name:"",
        email:"",
        password:"",
        password_confirmation:""
      }),
      alert:null
    }
  },
  methods:{
    submit(){
      self=this;
      this.form.post(`/register`)
      .then(res=>{
        console.log(res);
        if(res.status==200){
          this.alert="success";
        }
      })
      .catch(error=>{
        console.log(error);
      })
    }
  }
}
</script>