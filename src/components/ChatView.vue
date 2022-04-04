<template>
  <div class="flex-grow bg-pattern">
    <div class="section h-full">
      <ol class="h-full flex flex-col justify-end align-bottom p-2">
        <li
          v-for="(item, index) in items"
          :key="index"
          class="rounded border-4 border-gray-100 bg-gray-50 p-2 my-2"
        >
          {{ item.msg }}
        </li>
      </ol>
    </div>
  </div>
  <div class="p-5 border border-t-2 border-x-0 border-b-0 border-solid">
    <div class="mt-1 flex rounded-md shadow-sm">
      <div class="relative flex items-stretch flex-grow focus-within:z-10">
        <input
          type="text"
          class="focus:outline-none block w-full pl-2 sm:text-sm bg-gray-50"
          placeholder="Send your message ..."
          v-model="input"
          @keydown.enter="send"
        />
      </div>
      <button
        type="button"
        @click="send"
        class="-ml-px relative inline-flex items-center space-x-2 px-4 py-2 border border-gray-50 text-sm font-medium rounded-r-md text-gray-700 bg-gray-50 hover:bg-gray-100 focus:outline-none focus:ring-1 focus:ring-gray-100 focus:border-gray-100"
      >
        <PaperAirplaneIcon class="h-5 w-5 text-gray-400" aria-hidden="true" />
        <span>Send</span>
      </button>
    </div>
  </div>
</template>

<script>
import { PaperAirplaneIcon } from "@heroicons/vue/solid";

export default {
  name: "ChatView",
  components: {
    PaperAirplaneIcon,
  },
  data() {
    return {
      input: "",
      items: [],
      socketConnection: null,
    };
  },
  mounted() {
    // Calling onconnect Lambda function via API endpoint
    const instance = this;
    const connection = new WebSocket(
      process.env.VUE_APP_WEB_SOCKET_API_ENDPOINT
    );
    this.socketConnection = connection;
    connection.onopen = function (e) {
      console.log("onopen");
      console.dir(e);
    };
    connection.onerror = function (error) {
      console.error("onerror");
      console.dir(error);
    };
    connection.onmessage = function (e) {
      console.log("onmessage");
      console.dir(e);
      if (e && e.data) {
        instance.items.push({ msg: e.data });
      }
    };
    connection.onclose = function () {
      console.log("onclose");
    };
  },
  methods: {
    // Calling sendmessage Lambda function via API endpoint
    send: function () {
      this.socketConnection.send(
        JSON.stringify({
          action: "sendmessage",
          data: this.input,
        })
      );
      this.input = "";
    },
    disconnect: function () {
      // Calling ondisconnect Lambda function via API endpoint
      this.socketConnection.disconnect();
    },
  },
};
</script>
