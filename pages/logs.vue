<template>
  <div class="bg-white h-screen">
    <div class="text-[#0F102C] font-[700] text-2xl p-5">Logs</div>
    <div class="flex flex-wrap p-4">
      <div
        v-for="(item, index) of logs"
        :key="index"
        class="max-w-sm bg-white rounded-lg border border-gray-200 shadow-md m-3 hover:bg-gray-100 cursor-pointer"
      >
        <div class="p-6">
          <p class="mb-3 font-normal text-gray-700 whitespace-normal">
            {{ item.data.firstName }} {{ item.data.lastName }}
          </p>
          <p class="text-gray-700 whitespace-normal">
            <span class="font-semibold">Course:</span>
            {{ item.data.courseName }}
          </p>
          <p class="text-gray-700 whitespace-normal">
            <span class="font-semibold">Duration:</span>
            {{ item.data.courseLength }}
          </p>
          <p class="text-gray-700 whitespace-normal">
            <span class="font-semibold">Grade:</span>
            {{ item.data.grade }}
          </p>

          <p class="text-gray-700 break-words">
            <span class="font-semibold">Previous Hash:</span>
            <span class="whitespace-normal flex flex-wrap">
              {{ item.previousHash }}</span
            >
          </p>
          <p class="text-gray-700 whitespace-normal break-words">
            <span class="font-semibold">Hash:</span>
            <span>{{ item.hash }}</span>
          </p>
          <p class="text-gray-700 whitespace-normal">
            <span class="font-semibold">Timestamp:</span>
            {{ item.timestamp }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      logs: [],
    };
  },
  mounted() {
    this.getLogs();
  },

  methods: {
    async getLogs() {
      const accessToken = localStorage.getItem("accessToken");

      axios
        .get("https://node-blockchain.onrender.com/user/uploads", {
          headers: {
            Authorization: `Bearer ${accessToken}`,
          },
        })
        .then((res) => {
          console.log(res.data.data, "logs");
          this.logs = res.data.data;
        })
        .catch((error) => {
          if (error.response.status === 401) {
            this.$router.push("/college/login");
          }
        });
    },
  },
};
</script>
<style>
.break-words {
  word-break: break-all;
}
</style>
