<template>
  <div class="container text-centre">
    <h4>Welcome</h4>
    <h1 class="lead bold">We're excited to see what you can do!</h1>
    <div class="spacer-l"></div>
    <button
      class="btn btn-large"
      @click="$emit('updateCurrentComponent', 'details')"
    >
      Begin
    </button>
  </div>
</template>

<script>
export default {
  name: "Welcome",
  mounted() {
    this.$parent.detailsFormData = {};
    this.$parent.aboutFormData = {};
  }
};
</script>
