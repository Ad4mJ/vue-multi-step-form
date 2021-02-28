<template>
  <div class="container">
    <h3 class="text-centre bold">Upload Your Documents</h3>
    <p class="text-centre">
      <small
        >Required feilds are marked by an astrisk<span class="text-primary"
          >*</span
        ></small
      >
    </p>
    <div class="spacer-l"></div>
    <FileUpload
      :type="'CV'"
      :required="true"
      v-on:addFile="addFile"
      v-on:removeFile="removeFile"
    ></FileUpload>
    <div class="spacer-l"></div>
    <FileUpload
      :type="'Cover Letter'"
      v-on:addFile="addFile"
      v-on:removeFile="removeFile"
    ></FileUpload>
    <div class="spacer-m"></div>
    <button
      class="btn pull-left"
      @click="$emit('updateCurrentComponent', 'about')"
    >
      Back
    </button>
    <button class="btn pull-right" @click="submitHandler">
      Submit Application
    </button>
  </div>
</template>

<script>
import FileUpload from "../components/FileUpload";

export default {
  name: "Upload",
  components: {
    FileUpload
  },
  data() {
    return {
      files: []
    };
  },
  methods: {
    addFile(file) {
      this.files.push(file);
    },
    removeFile(file) {
      const index = this.files.findIndex(file);
      this.files.splice(index, 1);
    },
    submitHandler() {
      // TODO Added validation (CV Required)
      this.$emit("submitApplication", this.files);
    }
  }
};
</script>
