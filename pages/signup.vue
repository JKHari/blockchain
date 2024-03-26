<template>
  <div class="bg-gray-10">
    <div class="flex justify-center h-screen w-screen items-center">
      <div class="w-full md:w-1/2 flex flex-col items-center">
        <!-- text signUp -->
        <h1 class="text-center text-2xl font-bold text-gray-600 mb-6">
          SIGN UP
        </h1>
        <div class="w-3/4 mb-6">
          <input
            v-model="user.username"
            class="w-full py-4 px-8 bg-slate-200 placeholder:font-semibold rounded hover:ring-1 outline-blue-500"
            placeholder="User Name"
          />
        </div>
        <!-- email input -->
        <div class="w-3/4 mb-6">
          <input
            v-model="user.email"
            class="w-full py-4 px-8 bg-slate-200 placeholder:font-semibold rounded hover:ring-1 outline-blue-500"
            placeholder="User Email"
          />
        </div>
        <!-- password input -->
        <div class="w-3/4 mb-6">
          <input
            v-model="user.password"
            class="w-full py-4 px-8 bg-slate-200 placeholder:font-semibold rounded hover:ring-1 outline-blue-500"
            placeholder="Password"
          />
        </div>

        <!-- button -->
        <div class="w-3/4 mt-4">
          <button
            @click="signUp()"
            class="py-4 bg-blue-400 w-full rounded text-blue-50 font-bold hover:bg-blue-700"
          >
            SIGN UP
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: {
        username: "",
        email: "",
        password: "",
      },
    };
  },
  methods: {
    signUp() {
      fetch("https://node-blockchain.onrender.com/register", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(this.user),
      }).then((data) => {
        if (data.error) {
          console.log("cant register");
        } else {
          this.$router.push("/");
        }
      });
    },
  },
};
</script>
