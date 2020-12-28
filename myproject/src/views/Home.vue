<template>
  <div class="home">
    <div class="bg-yellow-400 text-4xl font-quicksand sm:text-sm">This element was styled with Tailwind, and the font is from Google Fonts</div>
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "Home",
  components: {
    HelloWorld
  }
};
</script>
