<template>
  <div class="px-5">
    <div class="mt-[40px]">
      <div class="flex justify-between">
        <div class="text-[#0F102C] font-[700] text-2xl">Admin</div>
        <nuxt-link
          :to="'/admin/logs'"
          class="font-[700] text-md bg-blue-600 px-4 rounded-md cursor-pointer py-2 text-white"
        >
          Logs
        </nuxt-link>
      </div>
    </div>
    <div class="flex flex-col mt-6">
      <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="inline-block min-w-full py-2 align-middle md:px-6 lg:px-8">
          <div class="overflow-hidden md:rounded-lg">
            <table class="min-w-full">
              <thead class="bg-slate-300">
                <tr>
                  <th
                    class="py-3.5 px-4 text-sm font-normal text-left rtl:text-right text-black"
                  >
                    <span>NO</span>
                  </th>
                  <th
                    class="px-12 py-3.5 text-sm font-normal text-left rtl:text-right text-black"
                  >
                    First Name
                  </th>
                  <th
                    scope="col"
                    class="px-4 py-3.5 text-sm font-normal text-left rtl:text-right text-black"
                  >
                    Last Name
                  </th>
                  <th
                    scope="col"
                    class="px-4 py-3.5 text-sm font-normal text-left rtl:text-right text-black"
                  >
                    Course Name
                  </th>
                  <th
                    scope="col"
                    class="px-4 py-3.5 text-sm font-normal text-left rtl:text-right text-black"
                  >
                    Course Duration
                  </th>
                  <th
                    scope="col"
                    class="px-4 py-3.5 text-sm font-normal text-left rtl:text-right text-black"
                  >
                    Grade
                  </th>
                  <th
                    scope="col"
                    class="px-4 py-3.5 text-sm font-normal text-left rtl:text-right text-black"
                  >
                    Action
                  </th>
                </tr>
              </thead>
              <tbody class="divide-y divide-gray-200 bg-white">
                <tr v-for="(item, index) of data" :key="index">
                  <td class="px-12 py-4 text-sm font-medium whitespace-nowrap">
                    <div class="text-black/70">{{ item.key }}</div>
                  </td>
                  <td class="px-12 py-4 text-sm font-medium whitespace-nowrap">
                    <div class="text-black/70">
                      {{ item.value.data.firstName }}
                    </div>
                  </td>
                  <td class="px-4 py-4 text-sm whitespace-nowrap">
                    <div>
                      <h4 class="text-black/70">
                        {{ item.value.data.lastName }}
                      </h4>
                    </div>
                  </td>
                  <td class="px-4 py-4 text-sm whitespace-nowrap">
                    <div>
                      <h4 class="text-black/70">
                        {{ item.value.data.courseName }}
                      </h4>
                    </div>
                  </td>
                  <td class="px-4 py-4 text-sm whitespace-nowrap">
                    <div>
                      <h4 class="text-black/70">
                        {{ item.value.data.courseLength }}
                      </h4>
                    </div>
                  </td>
                  <td class="px-4 py-4 text-sm whitespace-nowrap">
                    <div>
                      <h4 class="text-black/70">{{ item.value.data.grade }}</h4>
                    </div>
                  </td>

                  <td class="flex gap-2 justify-around mt-2">
                    <div
                      v-if="item.value.data.status === 'pending'"
                      class="px-4 py-2 text-xs bg-green-400 rounded-md text-white cursor-pointer hover:bg-green-500"
                      @click="statusUpdate(item.key, 'approved')"
                    >
                      Approve
                    </div>
                    <div
                      v-if="item.value.data.status === 'pending'"
                      class="px-4 py-2 text-xs bg-red-400 rounded-md text-white cursor-pointer hover:bg-red-500"
                      @click="statusUpdate(item.key, 'rejected')"
                    >
                      Reject
                    </div>
                    <div
                      v-if="item.value.data.status === 'approved'"
                      class="px-4 py-2 text-sm text-green-400 rounded-md"
                    >
                      Approved
                    </div>
                    <div
                      v-if="item.value.data.status === 'rejected'"
                      class="px-4 py-2 text-sm text-red-400 rounded-md"
                    >
                      Rejected
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
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
      data: [],
    };
  },
  mounted() {
    this.getData();
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
    async getData() {
      const admin_accessToken = localStorage.getItem("accessToken");
      if (!admin_accessToken) {
        this.$router.push("/admin/login");
      }
      try {
        axios
          .get("http://localhost:5000/data", {
            headers: {
              Authorization: `Bearer ${admin_accessToken}`,
            },
          })
          .then((res) => {
            this.data = res.data.data;
          });
      } catch (error) {
        console.log(error);
      }
    },
    statusUpdate(id, status) {
      console.log(id, status);

      axios
        .post(
          `http://localhost:5000/admin/status`,
          {
            id: id,
            status: status,
          },
          {
            headers: {
              Authorization: `Bearer ${localStorage.getItem(
                "admin_accessToken"
              )}`,
            },
          }
        )
        .then((res) => {
          console.log(res);
          this.getData();
        });
    },
  },
};
</script>