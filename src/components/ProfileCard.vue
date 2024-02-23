<script setup lang="ts">
import { defineProps } from 'vue';
interface UserProfile{
  avatar_url:string,
  name:string,
  login:string,
  created_at:string,
  bio:string,
  followers:number
}
const props=defineProps<{
  profile:UserProfile;
}>()

function extractYear(dateString: string): number {
  const dateObject = new Date(dateString);
  const year = dateObject.getFullYear();
  return year;
}

</script>

<template>  
  <div class="ui card">
    <div class="image">
      <img :src="props.profile.avatar_url">
    </div>
    <div class="content">
      <a class="header">{{ profile.name? profile.name:profile.login }}</a>
      <div class="meta">
        <span class="date">Joined in {{ extractYear(profile.created_at) }}</span>
      </div>
      <div class="description">
        {{ profile.bio }}
      </div>
    </div>
    <div class="extra content">
      <a>
        <i class="user icon"></i>
        {{ profile.followers }} Friends
      </a>
    </div>
  </div>
</template>

<style scoped></style>
