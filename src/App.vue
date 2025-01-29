<template>
  <div class="parent" ref="parent">
    <header>
      <h1>LOGO - {{ wih }} - {{ wvh }}</h1>
    </header>
    <iframe ref="iframe" src="https://staging.sports-aio-web.7platform.net/home?tenantId=0c17fe55-315e-4ee0-b4f6-1364c8557dd1&currency=eur&language=en&externalId=josipb&feToken=c&debug=true&standalone=true" id="child"></iframe>
  </div>
</template>

<script>
import { ref, onMounted, onBeforeUnmount } from "vue";

export default {
  setup() {
    const parent = ref(null);
    const iframe = ref(null);
    let lastScrollY = 0;
    let isAddressBarHidden = false;
    const wih = ref(0);
    const wvh = ref(0);

    const handleScroll = () => {
      const currentScrollY = window.scrollY;
      const viewportHeight = window.visualViewport.height;
      const windowHeight = window.innerHeight;
      wvh.value = viewportHeight;
      wih.value = windowHeight;
      console.log('test', wvh.value, wih.value);

      const scrollingDown = currentScrollY > lastScrollY;

      if (!isAddressBarHidden) {
        // Ako je address bar još uvek vidljiv
        if (viewportHeight < windowHeight) {
          isAddressBarHidden = true;
          enableIframeScroll();
        }
      } else {
        // Ako je address bar sakriven i korisnik skroluje gore, ponovo preuzmi kontrolu
        if (!scrollingDown) {
          isAddressBarHidden = false;
          disableIframeScroll();
        }
      }

      lastScrollY = currentScrollY;
    };

    const enableIframeScroll = () => {
      if (!iframe.value) return;
      iframe.value.style.pointerEvents = "auto"; // Omogućava interakciju sa `iframe`
    };

    const disableIframeScroll = () => {
      if (!iframe.value) return;
      iframe.value.style.pointerEvents = "none"; // Onemogućava interakciju sa `iframe`
      window.scrollTo({ top: 1, behavior: "instant" }); // Sprečava skokove
    };

    onMounted(() => {
      window.addEventListener("scroll", handleScroll, { passive: true });
    });

    onBeforeUnmount(() => {
      window.removeEventListener("scroll", handleScroll);
    });

    return { parent, iframe, wvh, wih };
  },
};
</script>

<style scoped>
.parent {
  width: 100%;
  height: calc(100dvh + 3000px);
}

header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background: blue;
  z-index: 10;
  height: 48px;
}

iframe {
  width: 100%;
  position: fixed;
  top: 48px;
  height: calc(100dvh - 100px);
  border: none;
  pointer-events: none; /* Početno isključujemo interakciju */
}
</style>
