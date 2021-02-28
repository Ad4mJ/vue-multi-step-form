<template>
  <div class="container">
    <h3 class="text-centre bold">More About You</h3>
    <p class="text-centre">
      <small
        >Required feilds are marked by an astrisk<span class="text-primary"
          >*</span
        ></small
      >
    </p>

    <FormulateForm
      class="custom-form"
      v-model="formValues"
      @submit="submitHandler"
    >
      <FormulateInput
        type="select"
        name="live_in_uk"
        label="Do You Live In The UK?"
        :options="{ Yes: 'Yes', No: 'No' }"
        validation="required"
        validation-name="this field"
        class="required"
      />
      <FormulateInput
        type="text"
        name="git_profile"
        label="Your Github Profile"
        validation="required"
        validation-name="this field"
        class="required"
      />
      <FormulateInput
        type="textarea"
        name="about_you"
        label="About You"
        validation-name="this field"
        validation="required"
        placeholder="Let us know more about you. What are you into?"
        class="required"
      />
      <FormulateInput
        type="button"
        label="Back"
        class="pull-left"
        @click="goBack"
      />
      <FormulateInput type="submit" label="Next" />
    </FormulateForm>
  </div>
</template>

<script>
export default {
  name: "About",
  data() {
    return {
      formValues: {}
    };
  },
  methods: {
    submitHandler() {
      this.$emit("saveOrUpdateAbout", this.formValues);
    },
    goBack() {
      this.$emit("updateCurrentComponent", "details");
    }
  },
  mounted() {
    this.formValues = this.$parent.aboutFormData;
  }
};
</script>
