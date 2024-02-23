<!-- layout that contain all component for main page -->

<script setup lang="ts">
//imports
import { ref } from 'vue'
import InputUser from '../components/InputUser.vue'
import ProfileCard from '../components/ProfileCard.vue'
import axios from 'axios'
import { toast } from 'vue3-toastify'
import 'vue3-toastify/dist/index.css'
//variables for error and save user data
const ProfileData = ref(null)
const errorMessage = ref('')

//function for fetch user data from github api
const getProfile = async (user: { name: string }) => {
  //try catch for error handling
  try {
    const response = await axios.get(`https://api.github.com/users/${user}`)
    ProfileData.value = response.data

    //this is for toast notification
    toast('Success', {
      theme: 'colored',
      type: 'success',
      hideProgressBar: true,
      dangerouslyHTMLString: true,
      autoClose: 1000
    })
  } catch (error: any) {
    if (error.response.status === 404) {
      errorMessage.value = 'user not found'

      toast(errorMessage.value, {
        theme: 'colored',
        type: 'error',
        hideProgressBar: true,
        dangerouslyHTMLString: true,
        autoClose: 1000
      })
    } else {
      errorMessage.value = 'server side error'

      toast(errorMessage.value, {
        theme: 'colored',
        type: 'error',
        hideProgressBar: true,
        dangerouslyHTMLString: true,
        autoClose: 1000
      })
    }
    ProfileData.value = null
  }
}
</script>

<template>
  <div class="wrapper">
    <div class="input-wrapper">
      <InputUser @findUser="getProfile" />
    </div>
    <div v-if="ProfileData" class="profile-card">
      <ProfileCard :profile="ProfileData" />
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.input-wrapper {
  width: 50%;
  text-align: center;
}
.error-message {
  font-size: 1.3rem;
  border: 1px solid red;
  width: 50%;
  color: red;
}
.profile-card {
  margin: 20px;
}
</style>
