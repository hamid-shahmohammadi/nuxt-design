<template>
  <div>
    <h1>index</h1>
    <p>{{$auth.loggedIn}}</p>
    
    
  </div>
</template>

<script>
export default {
  mounted() {
    console.log(this.$auth)
  }
};
</script>