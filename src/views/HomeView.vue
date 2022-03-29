<template>
  <div class="mx-auto w-full">
    <div class="grid grid-cols-3 gap-8 h-full pt-5">
      <div class="sm:invisible md:col-span-1"></div>
      <div class="col-span-3 md:col-span-1"><HelloWorld /></div>
      <div class="sm:invisible md:col-span-1 sm:hidden"></div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "HomeView",
  components: {
    HelloWorld,
  },
};
</script>
