<template>
  <div class="flex-grow">
    <div class="section">
      <ol>
        <li v-for="(item, index) in items" :key="index">
          {{ item.msg }}
        </li>
      </ol>
    </div>
  </div>
  <div class="py-5 border border-t-2 border-x-0 border-b-0 border-solid">
    <div class="flex items-start space-x-4">
      <div class="flex-shrink-0">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="inline-block h-10 w-10 rounded-full text-gray-500"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          stroke-width="2"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M5.121 17.804A13.937 13.937 0 0112 16c2.5 0 4.847.655 6.879 1.804M15 10a3 3 0 11-6 0 3 3 0 016 0zm6 2a9 9 0 11-18 0 9 9 0 0118 0z"
          />
        </svg>
      </div>
      <div class="min-w-0 flex-1">
        <div class="relative">
          <div
            class="border border-gray-300 rounded-lg shadow-sm overflow-hidden focus-within:border-indigo-500 focus-within:ring-1 focus-within:ring-indigo-500"
          >
            <label for="comment" class="sr-only">Add your comment</label>
            <textarea
              rows="3"
              name="comment"
              id="comment"
              class="block w-full p-5 border-0 resize-none focus:outline-none sm:text-sm"
              placeholder="Add your comment..."
              v-model="input"
            />

            <!-- Spacer element to match the height of the toolbar -->
            <div class="py-2" aria-hidden="true">
              <!-- Matches height of button in toolbar (1px border + 36px content height) -->
              <div class="py-px">
                <div class="h-9" />
              </div>
            </div>
          </div>

          <div
            class="absolute bottom-0 inset-x-0 pl-3 pr-2 py-2 flex justify-between"
          >
            <div class="flex items-center space-x-5">
              <div class="flex items-center"></div>
            </div>
            <div class="flex-shrink-0">
              <button
                type="button"
                class="inline-flex items-center px-4 py-2 border border-transparent text-sm font-medium rounded-md shadow-sm text-white bg-gray-600 hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-gray-500"
                @click="send"
              >
                Send
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ChatView",
  data() {
    return {
      input: "",
      msgs: "",
      items: [],
      socketConnection: null,
    };
  },
  mounted() {
    console.log(process.env);
    const that = this;
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
        that.msgs = e.data;
        that.items.unshift({ msg: e.data });
      }
    };
    connection.onclose = function () {
      console.log("onclose");
    };
  },
  methods: {
    send: function () {
      this.socketConnection.send(
        JSON.stringify({
          action: "sendmessage",
          data: this.input,
        })
      );
    },
    disconnect: function () {
      this.socketConnection.disconnect();
    },
  },
};
</script>
