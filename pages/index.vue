<template>
  <div>
    <div class="text-[#0F102C] font-[700] text-2xl p-5">Search Certificate</div>
    <div class="w-full flex justify-end md:pr-5">
      <div class="flex">
        <label for="simple-search" class="sr-only">Search</label>
        <div class="relative w-full">
          <input
            type="text"
            v-model="search"
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-gray-500 focus:border-gray-500 block w-full ps-10 p-2.5 outline-none"
            placeholder="Search "
            required
          />
        </div>
        <button
          @click="searchFilter()"
          class="p-2.5 ms-2 text-sm font-medium text-white bg-blue-700 rounded-lg border border-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300"
        >
          <svg
            class="w-4 h-4"
            aria-hidden="true"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 20 20"
          >
            <path
              stroke="currentColor"
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z"
            />
          </svg>
          <span class="sr-only">Search</span>
        </button>
      </div>
    </div>
    <div class="mt-8" v-if="data !== null">
      <div
        class="relative mx-auto bg-[#618597] p-8 text-[#333] font-sans shadow-md flex justify-center items-center"
        style="width: 800px; height: 600px"
      >
        <div class="absolute">
          <div
            class="border-2 border-white absolute"
            style="
              width: 794px;
              height: 594px;
              transform: translate(-50%, -50%);
            "
          />
          <div
            class="border-2 border-white absolute"
            style="
              width: 730px;
              height: 530px;
              transform: translate(-50%, -50%);
            "
          />

          <div
            class="absolute border bg-white p-0"
            style="
              width: 720px;
              height: 520px;
              transform: translate(-50%, -50%);
            "
          >
            <!-- Certificate Header -->
            <div class="font-pinyon text-center mt-10">
              <h2 class="font-pinyonScript text-5xl">
                Certificate of Completion
              </h2>
            </div>

            <!-- Certificate Body -->
            <div class="px-5 mt-12">
              <!-- Name Section -->
              <div class="flex justify-center">
                <div
                  class="text-center border-b-2 border-gray-700 py-2 mb-4"
                  style="width: 80%"
                >
                  <span class="font-bold text-xl"
                    >{{ data.firstName }}{{ data.lastName }}</span
                  >
                </div>
              </div>

              <!-- Course and Credit Section -->
              <div class="text-center mt-3">
                <span class="block font-pinyonScript text-xl">has earned</span>
                <span class="block font-bold"
                  >{{ data.courseName }}: {{ data.courseLength }} Credit
                  Hours</span
                >
              </div>

              <div class="text-center mt-2">
                <span class="block font-pinyonScript text-xl"
                  >while completing the training course entitled</span
                >
              </div>

              <div class="flex justify-center mt-1">
                <div
                  class="text-center border-b-2 border-gray-700 py-2"
                  style="width: 80%"
                >
                  <span class="block font-bold"
                    >BPS PGS Initial PLO for Principals at Cluster
                    Meetings</span
                  >
                </div>
              </div>
            </div>

            <!-- Footer -->
            <div class="absolute bottom-5 w-full">
              <div class="flex">
                <div class="flex justify-end pr-10 w-full text-sm">
                  <div class="text-center">
                    <span class="block">Date Completed</span>
                    <div
                      class="border-b-2 border-gray-700 my-2"
                      style="height: 30px"
                    >
                      {{ data.endDate.split(" ")[1] }}
                      {{ data.endDate.split(" ")[2] }}
                      {{ data.endDate.split(" ")[3] }}
                    </div>
                    <span class="block font-bold"
                      >Provider User Id # ({{ data.userId }})</span
                    >
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import { useToast } from "vue-toastification";
export default {
  data() {
    return {
      toast: useToast(),
      search: "",
      data: null,
    };
  },

  mounted() {
    // const accessToken = localStorage.getItem("accessToken");
    // console.log(accessToken);
    // if (!accessToken) {
    //   this.$router.push("/college/login");
    // }
    console.log("mounted", this.data);
  },

  methods: {
    async searchFilter() {
      try {
        const response = await axios.get(
          `https://node-blockchain.onrender.com/search?id=${this.search}`
        );
        if (response.data.success) {
          this.data = response.data.data;
        } else {
          this.toast.error(response.data.message);
        }
        console.log(this.data);
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>



