<script setup>
import { RouterLink, RouterView, useRouter } from 'vue-router'
const router = useRouter()
function goHome() {
router.push('/')
}
</script>

<template>
<nav>
<h1>{{$route.params.myjourney}}</h1>
<button @click="goHome()">GO HOME</button>
</nav>
</template>