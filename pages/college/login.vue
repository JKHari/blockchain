<template>
  <div class="bg-gray-10">
    <div class="flex justify-center h-screen w-screen items-center">
      <div class="w-full md:w-1/2 flex flex-col items-center">
        <!-- text login -->
        <h1 class="text-center text-2xl font-bold text-gray-600 mb-6">LOGIN</h1>
        <!-- email input -->
        <div class="w-3/4 mb-6">
          <input
            v-model="user.email"
            class="w-full py-4 px-8 bg-slate-200 placeholder:font-semibold rounded hover:ring-1 outline-blue-500"
            placeholder="Email"
          />
        </div>
        <!-- password input -->
        <div class="w-3/4 mb-6">
          <input
            v-model="user.password"
            type="password"
            class="w-full py-4 px-8 bg-slate-200 placeholder:font-semibold rounded hover:ring-1 outline-blue-500"
            placeholder="Password"
          />
        </div>
        <!-- remember input -->
        <div class="w-3/4 flex flex-row justify-between">
          <div class="flex items-center gap-x-1">
            <span class="text-sm text-slate-400">Dont Have an account</span>
          </div>
          <div>
            <p
              @click="gotoSignUp()"
              class="text-sm text-slate-400 hover:text-blue-500 cursor-pointer"
            >
              Register
            </p>
          </div>
        </div>
        <!-- button -->
        <div class="w-3/4 mt-4">
          <button
            @click="login()"
            class="py-4 bg-blue-400 w-full rounded text-blue-50 font-bold hover:bg-blue-700"
          >
            LOGIN
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { useToast } from "vue-toastification";

export default {
  data() {
    return {
      toast: useToast(),
      user: {
        email: "",
        password: "",
      },
    };
  },
  mounted() {
    const accessToken = localStorage.getItem("accessToken");
    if (accessToken) {
      this.$router.push("/dashboard");
    }
  },
  methods: {
    async login() {
      fetch("https://node-blockchain.onrender.com/login", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(this.user),
      }).then((res) => {
        if (res.status === 200) {
          res.json().then((data) => {
            console.log(data);
            localStorage.setItem("accessToken", data.accessToken);
            localStorage.setItem("refreshToken", data.refreshToken);
            this.toast.success("Login successful");
            this.$router.push("/dashboard");
          });
        } else {
          this.toast.error("Invalid email or password");
          console.log("Invalid email or password");
        }
      });
    },
    gotoSignUp() {
      this.$router.push("/signup");
    },
  },
};
</script>
