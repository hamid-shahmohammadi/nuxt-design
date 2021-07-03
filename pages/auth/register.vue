<template>
    <section class="authentication">
    <div class="auth-body">
      <h1 class="text-uppercase fw-500 mb-4 text-center font-22">Register</h1>
      <form class="auth-form" >
       
        <div class="form-group">
          <input
                class="form-control form-control-lg font-14 fw-300"
                type="text"
                name="name"
                placeholder="Full Name"
            />
        </div>
        <div class="form-group">
            <input
                class="form-control form-control-lg font-14 fw-300"
                type="text"
                name="username"
                placeholder="User Name"
            />
          
        </div>
        <div class="form-group">
          <input
                class="form-control form-control-lg font-14 fw-300"
                type="email"
                name="email"
                placeholder="Email"
          />
        </div>
        <div class="form-group">
          <input
                class="form-control form-control-lg font-14 fw-300"
                type="password"
                name="password"
                placeholder="Password"
          />
        </div>
        <div class="form-group">
            <input
                class="form-control form-control-lg font-14 fw-300"
                type="password"
                name="password_confirmation"
                placeholder="Confirm Password"
          />
        
        </div>

        <div class="text-right">
          <button type="submit" 
            class="btn btn-primary primary-bg-color font-16 fw-500 text-up">
            Register
          </button>
        </div>
        <p class="font-14 fw-400 text-center mt-4">
          Already have an account?
          <a class="color-blue">Login</a>
        </p>
      </form>
    </div>
  </section>
</template>