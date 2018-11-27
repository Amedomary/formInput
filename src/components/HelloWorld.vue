<template>
  <main class='wrapper'>
    <header>
      <p class='heading'>Login</p>
      <!-- <p class='create'>
        <a href='#'>Create account</a>
      </p> -->
    </header>

    <section class='avatar__section'>
      <transition name="avatar">
        <div class="avatar__row" v-if="state.userIsFound">

          <!-- НЕ ДЕЛАЙТЕ ТАК) -->

          <img class='avatar__pic' src='@/assets/ava.jpg' alt='' v-if="account === 1">
          <p class='avatar__text' v-if="account === 1">
            Wellcome back, Mila
          </p>

          <img class='avatar__pic' src='@/assets/ava1.jpg' alt='' v-if="account === 2">
          <p class='avatar__text' v-if="account === 2">
            Wellcome back, Tom
          </p>

          <img class='avatar__pic' src='@/assets/ava2.jpg' alt='' v-if="account === 3">
          <p class='avatar__text' v-if="account === 3">
            Wellcome back, Gal
          </p>
        </div>
      </transition>
    </section>

    <section class='input__row'>
      <div class='input__cell'>
        <label class='input__wrap'>
          <p class='username username--label'
             :class="state.unFocus ? 'focus' : ''"
          > Username </p>
          <input class='username username--input' type='text' value='' placeholder=''
                 v-bind:style="{fontSize: `${unFontSize}px`}"
                 ref="username_input"
                 v-on:focus="focusUser()"
                 v-on:blur="blurUser()"
                 v-on:input="inputUser()"
          >
        </label>
      </div>
      <hr class='input__separator'
          :class="state.searchUser ? 'search' : ''"
      />
      <div class='input__cell'>
        <label class='input__wrap'>
          <transition name="password">
            <p class='password password--label'
               :class="state.pwFocus ? 'focus' : ''"
               v-if="state.userIsFound"
            >Password</p>
          </transition>
          <input class='password password--input' type='password' value='' placeholder=''
                 ref="password_input"
                 v-if="state.userIsFound"
                 @focus="focusPassword()"
                 @input="inputPassword()"
                 @blur="blurPassword()"
          >
        </label>
      </div>
    </section>

    <section class="action__row">
      <div class="action__cell action__cell--next">
        <a class="action__link action__link--next" href="#" v-if="false">
          Next
        </a>
      </div>
      <div class="action__cell action__cell--singin">
        <transition name='singin'>
          <a class="action__link action__link--singin" href="#" v-if="state.pwComplete">
            Sing in
          </a>
        </transition>
      </div>
    </section>

    <footer>
      <p class='create'>
        <a class="create__link" href='#'>Forgot password?</a>
      </p>
      <p class='create'>
        <a class="create__link" href='#'>Create account</a>
      </p>
    </footer>
  </main>
</template>

<script>
export default {
  name: 'login',
  data() {
    return {
      unFontSize: 110,
      account: 1,
      state: {
        // un - user name
        // pw - pass word
        unFocus: false,
        unComplete: false,
        pwFocus: false,
        pwComplete: false,
        searchUser: false,
        userIsFound: false,
      },
    };
  },
  methods: {
    focusUser() {
      this.state.unFocus = true;
    },

    blurUser() {
    },

    inputUser() {
      // запускаем поиск аккаунта
      clearTimeout(this.timerId);
      this.state.userIsFound = false;
      if (this.$refs.username_input.value !== '') {
        this.state.unFocus = true;
        this.timerId = setTimeout(() => {
          this.searchUser();
        }, 500);
      } else {
        this.state.unFocus = false;
        this.state.pwFocus = false;
        this.state.pwComplete = false;
      }

      // Меняем размер шрифта
      if (this.$refs.username_input.value.length <= 7) {
        this.unFontSize = 110;
      } else if (this.$refs.username_input.value.length > 7 && this.unFontSize > 80) {
        this.unFontSize -= 6;
      }
    },

    searchUser() {
      this.state.searchUser = true;
      this.randomAccount();

      setTimeout(() => {
        this.state.searchUser = false;
        this.state.userIsFound = true;
      }, Math.random() * 800 + 200);
    },

    randomAccount() {
      const x = Math.random();
      if (x > 0.66) {
        this.account = 1;
      } else if (x > 0.33) {
        this.account = 2;
      } else {
        this.account = 3;
      }
    },

    focusPassword() {
      this.state.pwFocus = true;
    },

    blurPassword() {
      if (!this.$refs.password_input.value) {
        this.state.pwFocus = false;
      }
    },

    inputPassword() {
      clearTimeout(this.passId);
      if (this.$refs.password_input.value !== '') {
        this.state.pwFocus = true;
        this.passId = setTimeout(() => {
          this.state.pwComplete = true;
        }, 300);
      } else {
        this.state.pwFocus = false;
        this.state.pwComplete = false;
      }
    },
  },
};
</script>

<style scoped lang='scss'>
.wrapper {
  margin: auto;
  width: 100%;
  padding: 24px;
}

header {
  margin-bottom: 20px;
}

footer {
  margin-bottom: 100px;
}

.heading {
  text-align: center;
  font-size: 55px;
  font-family: "polar_vertexregular";
}

.avatar {
  &__section {
    height: 70px;
    margin-bottom: 20px;
  }

  &__row {
    display: flex;
    flex-flow: row nowrap;
    justify-content: center;
    align-items: center;
  }

  &__pic {
    height: 70px;
    width: 70px;
    display: block;
    border-radius: 75%;
    margin-right: 13px;
    object-fit: cover;
  }

  &__text {
    font-family: "Italianno", cursive;
    font-size: 45px;
    color: #ddd;
  }
}

.create {
  font-size: 28px;
  font-family: "Dancing Script", cursive;
  text-align: center;
  line-height: 30px;
  margin: 3px 0;

  &__link {
    display: inline-block;
    padding: 2px;
  }
}

.username {
  font-family: "anvylregular";
  font-size: 110px;
  text-align: right;
  position: absolute;
  top: 0;
  right: 0;
  left: 0;
  line-height: 113px;
  height: 113px;
  padding-right: 15px;

  &--label {
    cursor: pointer;
    opacity: 0.35;
    transition: 1s;

    &.focus {
      opacity: 0;
    }
  }

  &--input {
    color: #fff;
  }
}

.password {
  font-family: "anvylregular";
  font-size: 110px;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  line-height: 113px;
  height: 113px;
  padding-left: 15px;

  &--label {
    cursor: pointer;
    opacity: 0.35;
    transition: 1s;

    &.focus {
      opacity: 0;
    }
  }

  &--input {
    color: #fff;
  }
}

.input {
  &__row {
    display: flex;
    flex-flow: row nowrap;
    width: 100%;
    justify-content: center;
    align-items: stretch;
    margin-bottom: 25px;
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
    background-color: var(--white);

    &.search {
      overflow: hidden;
      position: relative;

      &:after {
        content: '';
        position: absolute;
        display: block;
        left: 0;
        right: 0;
        bottom: -60px;
        height: 60px;
        background-color: var(--accent);
        animation: separator_search  1s infinite linear;
      }
    }
  }

  &__wrap {
    display: block;
    width: 100%;
    height: 100%;
    position: relative;
  }
}

.action {
  &__row {
    display: flex;
    flex-flow: row nowrap;
    justify-content: center;
    align-items: stretch;
    margin-bottom: 25px;
    height: 66px;
  }

  &__cell {
    flex: 0 0 auto;
    width: 50%;
    padding: 0 15px;

    &--next {
      text-align: right;
    }
  }

  &__link {
    font-family: "Italianno", cursive;
    font-size: 45px;
    display: inline-block;
    padding: 5px;
    position: relative;
    transition: color 0.1s;

    &::after {
      content: "";
      position: absolute;
      width: 100%;
      height: 1px;
      background-image: linear-gradient(
        to right,
        rgba(255, 255, 255, 0),
        #ddd,
        #ddd,
        #ddd,
        rgba(255, 255, 255, 0)
      );
      bottom: 17px;
      left: 0;
    }

    &:hover {
      &:after {
        color: var(--accent);
        background-image: linear-gradient(
          to right,
          rgba(255, 255, 255, 0),
          var(--accent),
          #ddd,
          #ddd,
          rgba(255, 255, 255, 0)
        );
      }
    }
  }
}


// Анимации
.avatar {
  &-enter-active {
    transition: 1s;
    & * {
      transition: 1s;
    }
  }
  &-enter {
    & .avatar__pic {
      z-index: 25;
      opacity: 0;
      transform: translateX(100%);
    }
    & .avatar__text {
      z-index: 5;
      opacity: 0;
      transform: scale(.9);
    }
  }
  &-enter-to {
    & .avatar__pic {
      opacity: 1;
      transform: translateY(0);
    }
    & .avatar__text {
      opacity: 1;
      transform: scale(1);
    }
  }

  &-leave-active {
    transition: 1s;
    & * {
      transition: 1s;
    }
  }
  &-leave {
    & .avatar__pic {
      z-index: 25;
      opacity: 1;
      transform: translateX(0);
    }
    & .avatar__text {
      z-index: 5;
      opacity: 1;
      transform: scale(1);
    }
  }
  &-leave-to {
    & .avatar__pic {
      opacity: 0;
      transform: scale(.9) translateX(-35px);
    }
    & .avatar__text {
      opacity: 0;
      transform: scale(.9) translateX(35px);
    }
  }
}

.password {
  &-enter-active {
    transition: 1s;
  }
  &-enter {
    opacity: 0;
  }
  &-enter-to {
    opacity: 0.35;
  }
  &-leave-active {
    transition: 1s;
  }
  &-leave {
    opacity: 0.35;
  }
  &-leave-to {
    opacity: 0;
  }
}

.singin {
  &-enter-active {
    transition: 1s;
  }
  &-enter {
    opacity: 0;
  }
  &-enter-to {
    opacity: 1;
  }
  &-leave-active {
    transition: 1s;
  }
  &-leave {
    opacity: 1;
  }
  &-leave-to {
    opacity: 0;
  }
}

@keyframes separator_search {
  from {
    bottom: -60px;
  }
  to {
    bottom: 100%;
  }
}
</style>
