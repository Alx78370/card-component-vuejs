<script setup>
import { ref, onMounted } from 'vue';
const props = defineProps({
  username: { type: String, required: true }
})

const user = ref()

const fetchUser = async () => {
  const res = await fetch(`https://api.github.com/users/${props.username}`)
  const data = await res.json()
  user.value = data
}

onMounted(() => {
  fetchUser()
})
</script>

<template>
  <div v-if="user" class="card card-side bg-base-100 shadow-xl m-5">
  <figure>
    <img
      :src="user.avatar_url"
      :alt="'Profile picture ' + user.name" />
  </figure>
  <div class="card-body">
    <h2 class="card-title">{{ user.name }}</h2>
    <p>
      Followers: {{ user.followers }} <br>
      Following: {{ user.following }}
    </p>
    <div class="card-actions justify-end">
    <a :href="user.html_url" class="btn btn-primary" target="_blank">View Profile</a>
  </div>
  </div>
</div>
</template>
