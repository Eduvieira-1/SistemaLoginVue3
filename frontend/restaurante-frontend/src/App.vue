<template>
  <div>
    <template v-if="auth.isAuthenticated">
      Olá {{ auth.fullName }}
      <button @click="logout">logout</button>
    </template>
    <template v-else> Olá visitante </template>

    <router-view />
  </div>
</template>

<script setup>
import { useAuth } from "@/store/auth.js";
import { useRouter } from "vue-router";

const auth = useAuth();
const router = useRouter();

function logout() {
  auth.clear();
  router.push({ name: "login" });
}
</script>

<style lang="scss" scoped>
</style>