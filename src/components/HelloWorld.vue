<script setup lang="ts">
import { ref, computed } from 'vue'

defineProps<{ msg: string, }>()

const ip = ref("c8c9a3fbf278.local/m")
const httpContent = ref("noHttp")
// const count = ref(0)

function setIp(e: any) { console.log("set", e) }
async function fetchData() {

  httpContent.value = (await (await fetch(fetchAddr.value)).text());
  console.log(httpContent.value);
}

const fetchAddr = computed({
  get() {
    let addr = ip.value
    if (!addr.startsWith("http"))
      addr = "http://" + addr;
    return addr
  },
  set(_) { }
})

</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <input type="text" @change="setIp" :value="ip">
    <button type="button" @click="fetchData">fetchHttp</button>
    <iframe :src="fetchAddr"> </iframe>
    {{ httpContent }}
    <code>components/HelloWorld.vue</code> to test HMR

  </div>

  <p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank">create-vue</a>, the official Vue + Vite
    starter
  </p>
  <p>
    Install
    <a href="https://github.com/vuejs/language-tools" target="_blank">Volar</a>
    in your IDE for a better DX
  </p>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
