<script>
import TheFooter from "@/components/layout/TheFooter.vue";
import TheHeader from "@/components/layout/TheHeader.vue";
export default {
  components: {
    TheHeader,
    TheFooter
  }
};
</script>

<template>
  <TheHeader />
  <div id="MainContent">
    <RouterView />
  </div>
  <TheFooter />
</template>

<style lang="scss">
@font-face {
  font-family: iransansx;
  font-style: normal;
  font-weight: 100;
  src: url("assets/scss/fonts/woff/iransansx-thin.woff") format("woff"),
  url("assets/scss/fonts/woff2/iransansx-thin.woff2") format("woff2");
}

@font-face {
  font-family: iransansx;
  font-style: normal;
  font-weight: 200;
  src: url("assets/scss/fonts/woff/iransansx-ultralight.woff") format("woff"),
  url("assets/scss/fonts/woff2/iransansx-ultralight.woff2") format("woff2");
}

@font-face {
  font-family: iransansx;
  font-style: normal;
  font-weight: 300;
  src: url("assets/scss/fonts/woff/iransansx-light.woff") format("woff"),
  url("assets/scss/fonts/woff2/iransansx-light.woff2") format("woff2");
}

@font-face {
  font-family: iransansx;
  font-style: normal;
  font-weight: 500;
  src: url("assets/scss/fonts/woff/iransansx-medium.woff") format("woff"),
  url("assets/scss/fonts/woff2/iransansx-medium.woff2") format("woff2");
}

@font-face {
  font-family: iransansx;
  font-style: normal;
  font-weight: 600;
  src: url("assets/scss/fonts/woff/iransansx-demibold.woff") format("woff"),
  url("assets/scss/fonts/woff2/iransansx-demibold.woff2") format("woff2");
}

@font-face {
  font-family: iransansx;
  font-style: normal;
  font-weight: 800;
  src: url("assets/scss/fonts/woff/iransansx-extrabold.woff") format("woff"),
  url("assets/scss/fonts/woff2/iransansx-extrabold.woff2") format("woff2");
}

@font-face {
  font-family: iransansx;
  font-style: normal;
  font-weight: 900;
  src: url("assets/scss/fonts/woff/iransansx-black.woff") format("woff"),
  url("assets/scss/fonts/woff2/iransansx-black.woff2") format("woff2");
}

@font-face {
  font-family: iransansx;
  font-style: normal;
  font-weight: bold;
  src: url("assets/scss/fonts/woff/iransansx-bold.woff") format("woff"),
  url("assets/scss/fonts/woff2/iransansx-bold.woff2") format("woff2");
}

@font-face {
  font-family: iransansx;
  font-style: normal;
  font-weight: normal;
  src: url("assets/scss/fonts/woff/iransansx-regular.woff") format("woff"),
  url("assets/scss/fonts/woff2/iransansx-regular.woff2") format("woff2");
}
</style>
