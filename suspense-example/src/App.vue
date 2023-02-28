<template>
  <span class="error" v-if="err">{{ err }}</span>
  <suspense v-else>
    <template #default>
      <div>
        <Users />
        <hr />
        <Todos />
      </div>
    </template>
    <template #fallback>
      <div>Loading.......</div>
    </template>
  </suspense>
  <!-- <Users />
  <hr /> -->
</template>

<script setup>
import { onErrorCaptured, ref, defineAsyncComponent } from "@vue/runtime-core";
// import Todos from "./components/Todos.vue";
// import Users from "./components/User.vue";
const Users = defineAsyncComponent(() => import("./components/User.vue"));
const Todos = defineAsyncComponent(() => import("./components/Todos.vue"));
const err = ref(null);
onErrorCaptured(e => {
  err.value = e;
  return true;
});
</script>

<style scoped>
.error {
  color: red;
  font-size: 25px;
}
</style>
