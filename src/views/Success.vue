<template>
  <div class="container text-centre">
    <h4>Success!</h4>
    <h1 class="lead bold">Thank You</h1>
    <p>Our team will respond to you within the next 48h</p>
    <button class="btn" @click="$emit('updateCurrentComponent', 'welcome')">
      Home
    </button>
  </div>
</template>

<script>
export default {
  name: "Success"
};
</script>
