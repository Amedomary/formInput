<template>
  <div id='app'>
    <HelloWorld />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';

export default {
  name: 'app',
  components: {
    HelloWorld,
  },
};
</script>

<style lang='scss'>
  :root {
    --white: #c8c8c8;
    --black: #282828;
    --accent: rgb(161, 64, 64);
  }

  *,
  *:before,
  *:after {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    border: none;
    background: none;
    color: var(--white);
  }

  *:link,
  *:visited {
    color: inherit;
    text-decoration: none;
  }

  :first-letter {
    color: var(--accent);
  }

  html,
  body {
    min-height: 100%;
    height: 100%;
    font-size: 25px;
    margin: 0;
  }

  input {
    width: 100%;
    outline: none;

    &[type="text"] {
      text-overflow: ellipsis;
    }
  }

  a:hover {
    transition: color .15s;
    color: var(--accent);
  }

  #app {
    min-height: 100%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: flex-start;
    margin: 0;
    background-color: var(--black);
  }

  // 'Poiret One', cursive;

  // Шрифты
  @import url('https://fonts.googleapis.com/css?family=Aclonica|Amatic+SC|Bangers|Black+Han+Sans|Dancing+Script|Dokdo|Gamja+Flower|Gugi|Indie+Flower|Italianno|Lobster|Pattaya|Poiret+One|Rubik+Mono+One|Sigmar+One');

  @font-face {
    font-family: 'anvylregular';
    src: url('assets/fonts/anvyl-webfont.eot');
    src: url('assets/fonts/anvyl-webfont.eot?#iefix') format('embedded-opentype'),
      url('assets/fonts/anvyl-webfont.woff2') format('woff2'),
      url('assets/fonts/anvyl-webfont.ttf') format('truetype'),
      url('assets/fonts/anvyl-webfont.svg#anvylregular') format('svg');
    font-weight: normal;
    font-style: normal;
  }

  @font-face {
    font-family: 'polar_vertexregular';
    src: url('assets/fonts/polarvertex-regular-webfont.eot');
    src: url('assets/fonts/polarvertex-regular-webfont.eot?#iefix') format('embedded-opentype'),
      url('assets/fonts/polarvertex-regular-webfont.woff2') format('woff2'),
      url('assets/fonts/polarvertex-regular-webfont.ttf') format('truetype'),
      url('assets/fonts/polarvertex-regular-webfont.svg#polar_vertexregular') format('svg');
    font-weight: normal;
    font-style: normal;
  }

  body {
    font-family: 'Lobster', cursive;
    font-family: 'Amatic SC', cursive;
    font-family: 'Poiret One', cursive;
    font-family: 'Pattaya', sans-serif;
    font-family: 'Rubik Mono One', sans-serif;
    font-family: 'Black Han Sans', sans-serif;
    font-family: 'Indie Flower', cursive;
    font-family: 'Sigmar One', cursive;
    font-family: 'Bangers', cursive;
    font-family: 'Italianno', cursive;
    font-family: 'Dokdo', cursive;
    font-family: 'Gamja Flower', cursive;
    font-family: 'Gugi', cursive;
    font-family: 'Aclonica', sans-serif;
    font-family: 'Dancing Script', cursive;
  }
</style>
