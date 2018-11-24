<template>
  <main class='wrapper'>
    <header>
      <p class='heading'>Login</p>
      <p class='create'>
        <a href='#'>Create account</a>
      </p>
    </header>

    <section class='avatar__section'>
      <transition name="avatar">
        <div class="avatar__row" v-if="state.userIsFound">
          <img class='avatar__pic' src='@/assets/ava.jpg' alt=''>
          <p class='avatar__text' >Wellcome back, Mila</p>
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
              v-if="state.userIsFound"
            >Password</p>
          </transition>
          <input class='password password--input' type='password' value='' placeholder=''
             v-if="state.userIsFound"
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
        <a class="action__link action__link--singin" href="#" v-if="false">
          Sing in
        </a>
      </div>
    </section>

    <footer>
      <p class='create'>
        <a href='#'>Forgot password?</a>
      </p>
    </footer>
  </main>
</template>

<script>
export default {
  name: "login",
  data() {
    return {
      state: {
        // un - user name
        // pw - pass word
        unFocus: false,
        unComplete: false,
        pwFocus: false,
        pwComplete: false,
        searchUser: false,
        userIsFound: false,
      }
    };
  },
  methods: {
    focusUser() {
      console.log(this);
      console.log(this.state.unFocus);
      
      this.state.unFocus = true;
    },

    blurUser() {
      // this.state.unFocus = false;
    },

    inputUser() {
      clearTimeout(this.timerId);
      if (this.$refs.username_input.value !== '') {
        this.timerId = setTimeout(() => {
          this.searchUser();
        }, 1000);
      }
    },

    searchUser() {
      this.state.searchUser = true;
      setTimeout(() => {
        this.state.searchUser = false;
        this.state.userIsFound = true;
      }, 3000);
      
    }
  },
  mounted() {
  }

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
  font-size: 25px;
  font-family: "Dancing Script", cursive;
  text-align: center;
  line-height: 30px;
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
        animation: separator_search  1.5s infinite linear;
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
      transform: translateX(150%);
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
  &-leave {
    opacity: 1;
  }
  &-leave-to {
    opacity: 0;
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


// Загрузка имени
// анимация на центральный элемент
// посдветка ошибки
// кнопка войти и далее