<script>
import { onMounted, onBeforeUnmount, ref } from "vue";

export default {
  setup() {
    const fixedDiv = ref(null);
    const fixedDivContent = ref(null);
    let lastScrollY = 0;
    let ticking = false;
    let addressBarHidden = false; // Praćenje statusa address bara

    const syncFixedScroll = () => {
      if (!ticking) {
        ticking = true;
        requestAnimationFrame(() => {
          if (fixedDivContent.value) {
            fixedDivContent.value.scrollTo({
              top: window.scrollY,
              behaviour: 'instant',
            }); // Sinhronizacija skrola
          }
          ticking = false;
        });
      }
    };

    const handleScroll = () => {
      const currentScrollY = window.scrollY;
      const scrollingDown = currentScrollY > lastScrollY;
      const scrollingUp = currentScrollY < lastScrollY;

      // Provera visine za status address bara
      const isAddressBarHidden = window.innerHeight === screen.height;

      if (isAddressBarHidden && !addressBarHidden) {
        // Address bar sakriven, ukloni sinhronizaciju
        stopSyncScroll();
        addressBarHidden = true;
      } else if (!isAddressBarHidden && addressBarHidden) {
        // Address bar ponovo vidljiv, uključi sinhronizaciju
        startSyncScroll();
        addressBarHidden = false;
      }

      // Uslovi za smer i status address bara
      if (!addressBarHidden && scrollingDown) {
        // Address bar nije sakriven i skrola se prema dole
        startSyncScroll();
      } else if (addressBarHidden && scrollingDown) {
        // Address bar sakriven i skrola se prema dole
        stopSyncScroll();
      } else if (addressBarHidden && scrollingUp) {
        // Address bar sakriven i skrola se prema gore
        startSyncScroll();
      } else if (!addressBarHidden && scrollingUp) {
        // Address bar nije sakriven i skrola se prema gore
        stopSyncScroll();
      }

      lastScrollY = currentScrollY;
    };

    const startSyncScroll = () => {
      // Uključi `pointer-events: none` i sinhronizaciju
      if (fixedDiv.value) {
        fixedDiv.value.style.pointerEvents = "none";
      }
      if (!ticking) {
        window.addEventListener("scroll", syncFixedScroll, { passive: true });
      }
    };

    const stopSyncScroll = () => {
      // Ukloni `pointer-events: none` i zaustavi sinhronizaciju
      if (fixedDiv.value) {
        fixedDiv.value.style.pointerEvents = "auto";
      }
      window.removeEventListener("scroll", syncFixedScroll);
    };

    onMounted(() => {
      fixedDivContent.value = fixedDiv.value.querySelector(".fixed-div-content");
      window.addEventListener("scroll", handleScroll, { passive: true });
    });

    onBeforeUnmount(() => {
      window.removeEventListener("scroll", handleScroll);
      stopSyncScroll();
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
  height: 200vh; /* Dovoljno sadržaja da omogući window scroll */
}

.fixed-div {
  position: fixed;
  top: 100px;
  left: 0;
  width: 100%;
  height: calc(100vh - 100px);
  background-color: aliceblue;
  overflow-y: auto; /* Skrolabilni sadržaj */
  pointer-events: none; /* Ignoriše interakcije mišem */
  color: red;
}



.main-content {
  margin-top: 150px; /* Dovoljno prostora za vidljivi sadržaj */
}
</style>
