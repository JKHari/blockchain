<template>
  <div class="relative">
    <div class="w-full p-5">
      <div class="mb-[40px]">
        <div class="flex justify-between">
          <div class="text-[#0F102C] font-[700] text-2xl">Dashboard</div>
          <div class="flex gap-2">
            <div
              class="bg-blue-400 text-white px-4 py-2 rounded-md cursor-pointer hover:bg-blue-500"
              @click="create()"
            >
              create
            </div>
            <nuxt-link
              :to="'/logs'"
              class="bg-blue-400 text-white px-4 py-2 rounded-md cursor-pointer hover:bg-blue-500"
            >
              Logs
            </nuxt-link>
          </div>
        </div>
      </div>

      <div class="overflow-x-auto">
        <table class="min-w-full w-full">
          <thead class="bg-slate-300">
            <tr>
              <th
                class="py-3.5 px-4 text-sm font-normal text-left rtl:text-right text-black"
              >
                <span>No</span>
              </th>
              <th
                class="px-4 py-3.5 text-sm font-normal text-left rtl:text-right text-black"
              >
                Id
              </th>
              <th
                class="px-4 py-3.5 text-sm font-normal text-left rtl:text-right text-black"
              >
                First Name
              </th>
              <th
                class="px-4 py-3.5 text-sm font-normal text-left rtl:text-right text-black"
              >
                Last Name
              </th>
              <th
                class="px-4 py-3.5 text-sm font-normal text-left rtl:text-right text-black"
              >
                Course Names
              </th>
              <th
                class="px-4 py-3.5 text-sm font-normal text-left rtl:text-right text-black"
              >
                Course Duration
              </th>
              <th
                class="px-4 py-3.5 text-sm font-normal text-left rtl:text-right text-black"
              >
                Grade
              </th>
              <th
                class="px-4 py-3.5 text-sm font-normal text-left rtl:text-right text-black"
              >
                Actions
              </th>
            </tr>
          </thead>
          <tbody class="divide-y divide-gray-200 bg-white">
            <tr v-for="(item, index) of uploads.data" :key="index">
              <td
                class="py-4 px-4 text-sm whitespace-nowrap font-medium text-black/70"
              >
                {{ index + 1 }}
              </td>
              <td
                class="py-4 px-4 text-sm whitespace-nowrap font-medium text-black/70"
              >
                {{ item.hash }}
              </td>
              <td class="py-4 px-4 text-sm font-medium whitespace-nowrap">
                <div>
                  <h2 class="font-medium text-black/70">
                    {{ item.data.firstName }}
                  </h2>
                </div>
              </td>
              <td class="py-4 px-4 text-sm font-medium whitespace-nowrap">
                <div class="text-black/70">{{ item.data.lastName }}</div>
              </td>
              <td class="py-4 px-4 text-sm font-medium whitespace-nowrap">
                <div class="text-black/70">{{ item.data.courseName }}</div>
              </td>
              <td class="py-4 px-4 text-sm font-medium whitespace-nowrap">
                <div class="text-black/70">{{ item.data.courseLength }}</div>
              </td>
              <td class="py-4 px-4 text-sm font-medium whitespace-nowrap">
                <div class="text-black/70">{{ item.data.grade }}</div>
              </td>
              <td
                class="py-4 px-4 text-sm cursor-pointer font-medium whitespace-nowrap"
              >
                <div
                  class="text-blue-400"
                  @click="previewImage(item.data.imagePath)"
                >
                  view
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
    <div
      v-if="showForm"
      class="absolute w-full z-10 h-screen overflow-hidden top-0 left-0"
    >
      <div
        class="min-h-screen bg-white p-0 sm:p-12 flex justify-center items-center"
      >
        <div
          class="mx-auto max-w-md px-6 py-12 bg-white border-0 shadow-lg sm:rounded-3xl"
        >
          <div class="flex justify-between">
            <h1 class="text-2xl font-bold mb-8">Certificate</h1>
            <h1
              class="text-gray-600 text-2xl font-bold mb-8 hover:text-gray-700 cursor-pointer"
              @click="closeForm()"
            >
              X
            </h1>
          </div>
          <form id="form" novalidate>
            <div class="flex gap-5">
              <div class="relative z-0 w-full mb-5">
                <input
                  v-model="certificate.firstName"
                  type="text"
                  placeholder="First Name "
                  required
                  class="pt-3 pb-2 block w-full px-0 mt-0 bg-transparent border-0 border-b-2 appearance-none focus:outline-none focus:ring-0 focus:border-black border-gray-200"
                />
              </div>

              <div class="relative z-0 w-full mb-5">
                <input
                  v-model="certificate.lastName"
                  type="text"
                  placeholder="Last Name "
                  class="pt-3 pb-2 block w-full px-0 mt-0 bg-transparent border-0 border-b-2 appearance-none focus:outline-none focus:ring-0 focus:border-black border-gray-200"
                />
              </div>
            </div>

            <div class="relative z-0 w-full mb-5">
              <input
                v-model="certificate.courseName"
                type="text"
                placeholder="Course Name"
                class="pt-3 pb-2 block w-full px-0 mt-0 bg-transparent border-0 border-b-2 appearance-none focus:outline-none focus:ring-0 focus:border-black border-gray-200"
              />
            </div>
            <div class="relative z-0 w-full mb-5">
              <input
                v-model="certificate.courseLength"
                type="text"
                placeholder="Course Length(hours) "
                class="pt-3 pb-2 block w-full px-0 mt-0 bg-transparent border-0 border-b-2 appearance-none focus:outline-none focus:ring-0 focus:border-black border-gray-200"
              />
            </div>
            <div class="">
              <div class="demo-date-picker">
                <div class="block">
                  <el-date-picker
                    v-model="certificate.startDate"
                    type="date"
                    placeholder="Start Date"
                    :size="size"
                    class="!w-[100%] cursor-pointer"
                  />
                </div>
              </div>
              <div class="demo-date-picker mt-6">
                <div class="block">
                  <el-date-picker
                    v-model="certificate.endDate"
                    type="date"
                    placeholder="End Date"
                    :size="size"
                    class="!w-[100%] cursor-pointer"
                  />
                </div>
              </div>
            </div>

            <div class="relative z-0 w-full mb-5 mt-4">
              <input
                v-model="certificate.grade"
                type="text"
                placeholder="Grade"
                class="pt-3 pb-2 block w-full px-0 mt-0 bg-transparent border-0 border-b-2 appearance-none focus:outline-none focus:ring-0 focus:border-black border-gray-200"
              />
            </div>
            <div class="relative z-0 w-full mb-5">
              <input type="file" @change="handleFileUpload" />
            </div>

            <button
              id="button"
              type="button"
              class="w-full px-6 py-3 mt-3 text-lg text-white transition-all duration-150 ease-linear rounded-lg shadow outline-none bg-pink-500 hover:bg-pink-600 hover:shadow-lg focus:outline-none cursor-pointer"
              @click="issueCertificate()"
            >
              Issue Certificate
            </button>
          </form>
        </div>
      </div>
    </div>
    <div>
      <div
        v-show="showImage"
        class="absolute w-full z-10 h-screen overflow-hidden top-0 left-0"
      >
        <div
          class="min-h-screen bg-white p-0 sm:p-12 flex justify-center items-center"
        >
          <div
            class="mx-auto max-w-md px-6 py-12 bg-white border-0 shadow-lg sm:rounded-3xl"
          >
            <div class="flex justify-between">
              <h1 class="text-2xl font-bold mb-8">Image</h1>
              <h1
                class="text-2xl font-bold text-gray-800 cursor-pointer hover:text-gray-500 mb-8"
                @click="closePreviewImage()"
              >
                X
              </h1>
            </div>
            <div class="relative z-0 w-full mb-5">
              <img
                :src="`https://node-blockchain.onrender.com/image/${path}`"
                alt="certificate"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { useToast } from "vue-toastification";
import axios from "axios";
export default {
  data() {
    return {
      toast: useToast(),
      files: [],
      showImage: false,
      uploads: [],
      path: "",
      showForm: false,
      certificate: {
        firstName: "",
        lastName: "",
        courseName: "",
        courseLength: "",
        startDate: "",
        endDate: "",
        grade: "",
        file: null,
      },
    };
  },
  mounted() {
    this.userData();
  },
  methods: {
    userData() {
      const accessToken = localStorage.getItem("accessToken");
      axios
        .get("https://node-blockchain.onrender.com/user/uploads", {
          headers: {
            Authorization: `Bearer ${accessToken}`,
          },
        })
        .then((response) => {
          this.uploads = response.data;
        })
        .catch((error) => {
          if (error.response.status === 401) {
            localStorage.removeItem("accessToken");
            this.$router.push("/college/login");
          }
        });
    },
    async issueCertificate() {
      this.showForm = false;
      const accessToken = localStorage.getItem("accessToken");
      if (!accessToken) return;

      const formData = new FormData();
      formData.append("firstName", this.certificate.firstName);
      formData.append("lastName", this.certificate.lastName);
      formData.append("courseName", this.certificate.courseName);
      formData.append("courseLength", this.certificate.courseLength);
      formData.append("startDate", this.certificate.startDate);
      formData.append("endDate", this.certificate.endDate);
      formData.append("grade", this.certificate.grade);
      formData.append("image", this.certificate.file); // Append the file

      try {
        const response = await axios.post(
          "https://node-blockchain.onrender.com/upload",
          formData,
          {
            headers: {
              "Content-Type": "multipart/form-data",
              Authorization: `Bearer ${accessToken}`,
            },
          }
        );
        console.log(response.data);
        this.toast.success("Certificate issued successfully");
        this.userData();
      } catch (error) {
        console.error("There was an error uploading the file:", error);
      }
    },
    create() {
      console.log("issueCertificate");
      this.showForm = true;
    },
    closeForm() {
      this.showForm = false;
    },
    async previewImage(path) {
      this.path = path;
      this.showImage = true;
    },
    closePreviewImage() {
      this.showImage = false;
    },
    handleFileUpload(event) {
      console.log(event.target.files[0]);
      this.certificate.file = event.target.files[0];
    },
  },
};
</script>
