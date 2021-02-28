<template>
  <div class="container">
    <h3 class="text-centre bold">Personal Details</h3>
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
        type="text"
        name="first_name"
        label="First Name"
        validation="bail|required"
        validation-name="this field"
        error-behavior="submit"
        class="required"
      />
      <FormulateInput type="text" name="last_name" label="Last Name" />
      <FormulateInput
        type="email"
        name="email"
        label="Email Address"
        validation="required"
        validation-name="this field"
        class="required"
      />
      <FormulateInput type="text" name="phone_number" label="Phone Number" />
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
  name: "Details",
  data() {
    return {
      formValues: {}
    };
  },
  methods: {
    submitHandler() {
      this.$emit("saveOrUpdateDetails", this.formValues);
    },
    goBack() {
      this.$emit("updateCurrentComponent", "welcome");
    },
    clearData() {
      this.$emit("updateCurrentComponent", "welcome");
    }
  },
  mounted() {
    this.formValues = this.$parent.detailsFormData;
  }
};
</script>
