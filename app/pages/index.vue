<template>
  <div class="fill-height d-flex align-center justify-center">
    <v-card width="520" class="pa-6 rouded-x1 elevation=60"></v-card>


    <div class="text-center mb-6"></div>
    <v-avatar size="90" class="=mb-3 elevation-3">
      <v-img :src="user?.picture" />
    </v-avatar>

    <h1>Hello World</h1>
    <v-btn>Submit</v-btn>
    <v-btn @click = "logout">Logout</v-btn>



    <h2 class = "text-h5 font-weight-bold mb-1">
  {{user?.name}}
</h2>

<p class="text-body-2 text-grey-">
  {{user?.email}}
</p>
  </div>
</template>




<script lang="ts" setup>
// @ts-nocheck
definePageMeta({
  middleware: 'auth'

})

const user  = ref<any>(null)
const showScanner = ref(false)
const scannedValue =ref('')

onMounted(() => {
  const savedUser = localStorage.getItem('google_user')

  if (!savedUser) {
    navigateTo('/login')
    return
  }

  user.value = JSON.parse(savedUser)
})


const logout = () => {
  localStorage.removeItem('google_user')
  localStorage.removeItem('google_token')
  window.google?.accounts.id.disableAutoSelect()
  navigateTo('/login')
}

</script>

<style>

</style>