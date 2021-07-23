<template>
  <div>
    <NavBar />
  
    <div class="container">
      <h1 class="mt-3">Welcome</h1>
      <p v-if="$auth.loggedIn">
        User: {{$auth.user.name}} <br> Email: {{$auth.user.email}}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  auth: false
}
</script>