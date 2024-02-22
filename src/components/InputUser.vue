<script setup lang="ts">

import { ref ,defineEmits} from 'vue';
const emit=defineEmits(['finduser']);
const username=ref("");
const getuser=()=>{
  emit('finduser',username.value);
}
</script>

<template>
  <h1>Search Github Profile</h1>
  <form action="" class="search-form" @submit.prevent="getuser">
    <div class="ui left icon input">
      <input type="text" placeholder="Search GitHub users..." style="width: 50vw;" v-model="username"/>
      <i class="users icon"></i>
    </div>
    <button type="submit" class="ui secondary button">
        <i class="search icon"></i>
    </button>
  </form>
</template>

<style scoped>
.search-form{
    width: 60%;
    display: flex;
    justify-content: space-between
}

</style>
