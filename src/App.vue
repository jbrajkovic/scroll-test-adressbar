<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'

function scrollToBottom() {
  window.scrollTo({
    behavior: 'smooth',
    top: document.body.scrollHeight
  })
}
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <button @click="scrollToBottom">SCROLL TO BOTTOM</button>
    <TheWelcome />
    <div class="scroll-trigger"></div>
    <div class="fixed-div">
      <div class="fixed-div-title">IFRAME</div>
      <div class="fixe-div-content">
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
        <div>TEST</div>
      </div>
    </div>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

.scroll-trigger {
  height: 1000px;
  width: 100%;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}

.fixed-div {
  position: fixed;
  top: 0;
  left: 0;
  background-color: aliceblue;
  width: 100%;
  height: 100dvh;
  color: #000;
}
</style>
