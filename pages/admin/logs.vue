<template>
  <div class="bg-white h-screen">
    <div class="text-[#0F102C] font-[700] text-2xl">Logs</div>
    <div class="flex flex-wrap p-4">
      <div
        v-for="(item, index) of logs"
        :key="index"
        class="max-w-sm bg-white rounded-lg border border-gray-200 shadow-md m-3 hover:bg-gray-100 cursor-pointer"
      >
        <div class="p-6">
          <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900">
            {{ item.key }}
          </h5>
          <p class="mb-3 font-normal text-gray-700 whitespace-normal">
            {{ item.value.data.firstName }} {{ item.value.data.lastName }}
          </p>
          <p class="text-gray-700 whitespace-normal">
            <span class="font-semibold">Course:</span>
            {{ item.value.data.courseName }}
          </p>
          <p class="text-gray-700 whitespace-normal">
            <span class="font-semibold">Duration:</span>
            {{ item.value.data.courseLength }}
          </p>
          <p class="text-gray-700 whitespace-normal">
            <span class="font-semibold">Grade:</span>
            {{ item.value.data.grade }}
          </p>
          <p class="text-gray-700 whitespace-normal">
            <span class="font-semibold">Status:</span>
            {{ item.value.data.status }}
          </p>
          <p class="text-gray-700 break-words">
            <span class="font-semibold">Previous Hash:</span>
            <span class="whitespace-normal flex flex-wrap">
              {{ item.value.previousHash }}</span
            >
          </p>
          <p class="text-gray-700 whitespace-normal break-words">
            <span class="font-semibold">Hash:</span>
            <span>{{ item.value.hash }}</span>
          </p>
          <p class="text-gray-700 whitespace-normal">
            <span class="font-semibold">Timestamp:</span>
            {{ item.value.timestamp }}
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
    const admin_accessToken = localStorage.getItem("admin_accessToken");
    if (
      admin_accessToken === null ||
      admin_accessToken === "" ||
      admin_accessToken === "undefined"
    ) {
      this.$router.push("/admin/login");
    }
  },

  methods: {
    async getLogs() {
      const admin_accessToken = localStorage.getItem("admin_accessToken");

      try {
        axios
          .get("http://localhost:5000/data", {
            headers: {
              Authorization: `Bearer ${admin_accessToken}`,
            },
          })
          .then((res) => {
            this.logs = res.data.data;
          });
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
<style>
.break-words {
  word-break: break-all;
}
</style>
