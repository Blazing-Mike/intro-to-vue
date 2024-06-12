<script setup>
const props = defineProps({
  open: Boolean
})
</script>

<template>
  <div v-if="open" class="modal-mask">
    <div class="modal-container">
      <div class="modal-body">
        <div class="modal-heading">
          <h1 class="heading">sign in</h1>
          <button class="close-modal-btn" @click="$emit('closeSignin')">close modal</button>
        </div>

        <form action="">
          <input type="text" placeholder="username" />
          <input type="password" placeholder="password" />
          <button type="submit">sign in</button>
        </form>
      </div>
    </div>
  </div>
</template>
