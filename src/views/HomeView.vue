<template>
  <div class="flex flex-col h-screen">
    <ChatView />
  </div>
</template>

<script>
// @ is an alias to /src
import ChatView from "@/components/ChatView.vue";

export default {
  name: "HomeView",
  components: {
    ChatView,
  },
};
</script>
