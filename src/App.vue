<script>
import { onMounted, onBeforeUnmount, ref } from "vue";

export default {
  setup() {
    const fixedDiv = ref(null);

    let ticking = false; // Flag za debouncing preko requestAnimationFrame

    const syncWindowScroll = (event) => {
      if (!ticking) {
        ticking = true;
        requestAnimationFrame(() => {
          window.scrollTo({
            top: event.target.scrollTop, // Sinkroniziraj window scroll
          });
          ticking = false;
        });
      }
    };

    onMounted(() => {
      if (fixedDiv.value) {
        fixedDiv.value.addEventListener("scroll", syncWindowScroll, {
          passive: true, // Poboljšava performanse
        });
      }
    });

    onBeforeUnmount(() => {
      if (fixedDiv.value) {
        fixedDiv.value.removeEventListener("scroll", syncWindowScroll);
      }
    });

    return {
      fixedDiv,
    };
  },
};
</script>



<template>
  <header>
    TEST
  </header>

  <main ref="mainElement">
    <div class="fixed-div" ref="fixedDiv">
      <div class="fixed-div-title">IFRAME</div>
      <div class="fixed-div-content">
        <div v-for="i in 100" :key="i">TEST {{ i }}</div>
      </div>
    </div>
    <div class="main-content">
      <div v-for="i in 100" :key="'main' + i">Main Content {{ i }}</div>
    </div>
  </main>
</template>

<style scoped>
header {
  width: 100%;
  height: 100px;
  background-color: orange;
}

main {
  height: calc(100dvh + 200px);
  overflow-y: auto; /* Osiguraj da main ima skrol */
}

.fixed-div {
  position: fixed;
  top: 100px;
  left: 0;
  background-color: aliceblue;
  width: 100%;
  height: 100dvh;
  color: #000;
  overflow-y: auto; /* Skrol za fixed div */
}

.main-content {
  padding-top: 100px;
}
</style>
