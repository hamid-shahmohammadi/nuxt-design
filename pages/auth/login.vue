<template>
    <section class="authentication">
    <div class="auth-body">
      <h1 class="text-uppercase fw-500 mb-4 text-center font-22">
        Login
      </h1>
      <form class="auth-form" >
        <div class="form-group">
            <input
                class="form-control form-control-lg font-14 fw-300"
                type="text"
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
        <div class="mt-4 mb-4 clearfix">
          <a
            
            class="forgot-pass color-blue font-14 fw-400"
          >
            Forgot password?
          </a>
        </div>
        <div class="text-right">
          <button type="submit" 
            class="btn btn-primary primary-bg-color font-16 fw-500 text-up">
            Login
          </button>
        </div>
        <p class="font-14 fw-400 text-center mt-4">
          Don't have an account yet?
          <a  class="color-blue">
            Create an account
          </a>
        </p>
      </form>
    </div>
  </section>
</template>