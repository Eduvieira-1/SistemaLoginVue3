<template>
  <div>
    <template v-if="!auth.isAuthenticated">
      <form @submit.prevent="login">
        <input v-model="user.email" type="text" placeholder="Seu email" />
        <input
          v-model="user.password"
          type="password"
          placeholder="Sua senha"
        />
        <button type="submit" @click="test">Login</button>
      </form>
    </template>
    <template v-else>
      <home />
    </template>
  </div>
</template>

<script setup>
import http from "@/services/http.js";
import { reactive } from "vue";
import { useAuth } from "@/store/auth.js";
import { useRouter } from "vue-router";
import Home from "../components/HomeStart.vue";

const auth = useAuth();

const user = reactive({
  email: "eduardo@icloud.com",
  password: "123",
});

const router = useRouter();
function test() {
  router.push({ name: "login" });
}

async function login() {
  try {
    const { data } = await http.post("/auth", user);
    console.log(data);
    auth.setToken(data.token);
    auth.setUser(data.user);
  } catch (error) {
    console.log(error?.response?.data);
  }
}
</script>

<style>
</style>