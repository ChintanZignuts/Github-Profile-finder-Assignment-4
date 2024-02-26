<!-- component for input field  -->

<script setup lang="ts">
import { ref, defineEmits } from 'vue'

const emit = defineEmits(['findUser'])
const username = ref<string>('')

const getUser = () => {
  emit('findUser', username.value)
}
</script>

<template>
  <h1>Search Github Profile</h1>
  <form action="" class="search-form" @submit.prevent="getUser">
    <div class="ui left icon input">
      <input type="text" placeholder="Search GitHub users..." v-model="username" />
      <i class="users icon"></i>
    </div>
    <button type="submit" class="ui secondary button">
      <i class="search icon"></i>
    </button>
  </form>
</template>

<style scoped>
input {
  width: 30vw;
  height: 50px;
  font-size: 1.2rem;
}
.search-form {
  display: flex;
  justify-content: center;
}
</style>
