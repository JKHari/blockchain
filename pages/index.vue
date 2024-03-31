<template>
  <div class="text-[#0F102C] font-[700] text-2xl p-5">Search Certificate</div>
  <div class="container pm-certificate-container">
    <div class="outer-border"></div>
    <div class="inner-border"></div>

    <div class="pm-certificate-border col-span-12">
      <div class="row pm-certificate-header">
        <div class="pm-certificate-title cursive col-span-12 text-center">
          <h2>Buffalo Public Schools Certificate of Completion</h2>
        </div>
      </div>

      <div class="row pm-certificate-body">
        <div class="pm-certificate-block">
          <div class="col-span-12">
            <div class="row">
              <div class="col-span-2"><!-- LEAVE EMPTY --></div>
              <div
                class="pm-certificate-name underline margin-0 col-span-8 text-center"
              >
                <span class="pm-name-text font-bold"
                  >TrueNorth Administrator</span
                >
              </div>
              <div class="col-span-2"><!-- LEAVE EMPTY --></div>
            </div>
          </div>

          <div class="col-span-12">
            <div class="row">
              <div class="col-span-2"><!-- LEAVE EMPTY --></div>
              <div class="pm-earned col-span-8 text-center">
                <span class="pm-earned-text padding-0 block cursive"
                  >has earned</span
                >
                <span class="pm-credits-text block font-bold sans"
                  >PD175: 1.0 Credit Hours</span
                >
              </div>
              <div class="col-span-2"><!-- LEAVE EMPTY --></div>
              <div class="col-span-12"></div>
            </div>
          </div>

          <div class="col-span-12">
            <div class="row">
              <div class="col-span-2"><!-- LEAVE EMPTY --></div>
              <div class="pm-course-title col-span-8 text-center">
                <span class="pm-earned-text block cursive"
                  >while completing the training course entitled</span
                >
              </div>
              <div class="col-span-2"><!-- LEAVE EMPTY --></div>
            </div>
          </div>

          <div class="col-span-12">
            <div class="row">
              <div class="col-span-2"><!-- LEAVE EMPTY --></div>
              <div class="pm-course-title underline col-span-8 text-center">
                <span class="pm-credits-text block font-bold sans"
                  >BPS PGS Initial PLO for Principals at Cluster Meetings</span
                >
              </div>
              <div class="col-span-2"><!-- LEAVE EMPTY --></div>
            </div>
          </div>
        </div>

        <div class="col-span-12">
          <div class="row">
            <div class="pm-certificate-footer">
              <div class="col-span-4 pm-certified col-span-4 text-center">
                <span class="pm-credits-text block sans"
                  >Buffalo City School District</span
                >
                <span class="pm-empty-space block underline"></span>
                <span class="font-bold block"
                  >Crystal Benton Instructional Specialist II, Staff
                  Development</span
                >
              </div>
              <div class="col-span-4">
                <!-- LEAVE EMPTY -->
              </div>
              <div class="col-span-4 pm-certified col-span-4 text-center">
                <span class="pm-credits-text block sans">Date Completed</span>
                <span class="pm-empty-space block underline"></span>
                <span class="font-bold block">DOB: </span>
                <span class="font-bold block"
                  >Social Security # (last 4 digits)</span
                >
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div>
    <div class="flex items-center max-w-sm mx-auto">
      <label for="simple-search" class="sr-only">Search</label>
      <div class="relative w-full">
        <input
          type="text"
          v-model="search"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full ps-10 p-2.5 dark:placeholder-gray-400"
          placeholder="Search "
          required
        />
      </div>
      <button
        @click="searchFilter()"
        class="p-2.5 ms-2 text-sm font-medium text-black bg-blue-700 rounded-lg border border-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300"
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
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      search: "",
      data: [],
    };
  },

  methods: {
    searchFilter() {
      try {
        const response = axios.get(
          `https://node-blockchain.onrender.com/search?id=${this.search}`
        );
        this.data = response.data;
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>

