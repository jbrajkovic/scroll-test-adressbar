<script>
import { onMounted, onBeforeUnmount, ref } from "vue";

export default {
  setup() {
    const fixedDiv = ref(null);
    let ticking = false; 

    const syncFixedScroll = () => {
      if (!ticking) {
        ticking = true;
        requestAnimationFrame(() => {
          if (fixedDiv.value) {
            fixedDiv.value.scrollTo({
              top: window.scrollY, 
              behavior: "instant", 
            });
          }
          ticking = false; 
        });
      }
    };

    onMounted(() => {
      window.addEventListener("scroll", syncFixedScroll, { passive: true });
    });

    onBeforeUnmount(() => {
      window.removeEventListener("scroll", syncFixedScroll);
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

  <main>
    <div class="fixed-div" ref="fixedDiv">
      <div class="fixed-div-title">Fixed Content</div>
      <div class="fixed-div-content">
        <div v-for="i in 100" :key="i">Fixed Content {{ i }}</div>
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
  height: 200vh; 
}

.fixed-div {
  position: fixed;
  top: 100px;
  left: 0;
  width: 100%;
  height: calc(100vh - 100px);
  background-color: aliceblue;
  overflow-y: auto; 
  pointer-events: none; 
  color: red;
}



.main-content {
  margin-top: 150px; 
}
</style>
