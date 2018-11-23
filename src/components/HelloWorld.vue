<template>
  <main class="wrapper">
    <header>
      <p class="heading">Login</p>
      <p class="create">
        <a href="#">Create account</a>
      </p>
    </header>

    <footer>
      <p> Forgot password ? </p>
    </footer>





    <p class="username"> AMedomary </p>
    <p> AMedomary </p>
    <p> ***** </p>
    <p> Create account </p>
    <p> Forgot password ? </p>
    
  </main>
</template>

<script>
export default {
  name: "login"
};
</script>

<style scoped lang="scss">
  .wrapper {
    margin: auto;
  }

  header {
    margin-bottom: 100px;
  }

  .heading {
    text-align: center;
    font-size: 55px;
    font-family: "polar_vertexregular";
  }

  .username {
    font-family: "anvylregular";
  }

  .create {
    font-size: 25px;
    font-family: "Dancing Script", cursive;
    text-align: center;
  }
</style>
