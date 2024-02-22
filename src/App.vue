<script setup lang="ts">
import { ref } from 'vue';
import InputUser from './components/InputUser.vue'
import ProfileCard from './components/ProfileCard.vue'
import axios from "axios"
const ProfilData=ref(null);
const errorMessage=ref('');
const getProfile=async (user:{name:string})=>{
  try {
    const response=await axios.get(`https://api.github.com/users/${user}`);
    ProfilData.value=response.data;
  } catch (error) {
    console.log(error);
    if(error.response.status===404){
      errorMessage.value="user not found"
    }
    else{
      errorMessage.value="server side error"
    }
    ProfilData.value=null;
  }
}
</script>

<template>
  <div class="wraper">
    <div class="input-wraper">
      <InputUser @finduser="getProfile"/>
    </div>
    <div v-if="ProfilData" class="profile-card">
      <ProfileCard :profile="ProfilData"/>
    </div>
    <div v-else-if="errorMessage" class="error-message">
      {{ errorMessage }}
    </div>
  </div>
</template>

<style scoped>
.wraper{
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.input-wraper{
  width: 50%;
  text-align: center;
}
.error-message{
  font-size: 1.3rem;
  border: 1px solid red;
  width: 50%;
  color: red;
}
.profile-card{
  margin: 20px;
}
</style>
