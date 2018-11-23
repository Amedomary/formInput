<template>
  <main class="wrapper">
    <header>
      <p class="heading">Login</p>
      <p class="create">
        <a href="#">Create account</a>
      </p>
    </header>

    <section class="input__row">
      <div class="input__cell">
        <label class="input__wrap">
          <p class="username username--label">Username</p>
          <input class="username username--input" type="text" value="" placeholder="">
        </label>
      </div>
      <hr class="input__separator" />
      <div class="input__cell">
        <label class="input__wrap">
          <p class="password password--label">Password</p>
          <input class="password password--input" type="password" value="" placeholder="">
        </label>
      </div>
    </section>

    <footer>
      <p class="create">
        <a href="#">Fargot password?</a>
      </p>
    </footer>
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
    width: 100%;
    padding: 24px;
  }

  header {
    margin-bottom: 100px;
  }

  footer {
    margin-bottom: 100px;
  }

  .heading {
    text-align: center;
    font-size: 55px;
    font-family: "polar_vertexregular";
  }

  .create {
    font-size: 25px;
    font-family: "Dancing Script", cursive;
    text-align: center;
  }

  .username {
    font-family: "anvylregular";
    font-size: 92px;
    text-align: right;
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;

    &--label {
      cursor: pointer;
      opacity: .3;
    }

    &--input {
      color: #ddd;
    }
  }

  .password {
    font-family: "anvylregular";
    font-size: 92px;
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;

    &--label {
      cursor: pointer;
      opacity: .3;
    }

    &--input {
      color: #ddd;
    }
  }

  .input {
    &__row {
      display: flex;
      flex-flow: row nowrap;
      width: 100%;
      justify-content: center;
      align-items: stretch;
      margin-bottom: 100px;
    }

    &__cell {
      flex: 0 0 auto;
      width: 50%;
    }

    &__separator {
      display: inline-block;
      flex: 0 0 auto;
      width: 3px;
      height: 124px;
      margin: 0 15px;
      background-color: var(--white);
    }

    &__wrap {
      display: block;
      width: 100%;
      height: 100%;
      position: relative;
    }
  }
</style>
