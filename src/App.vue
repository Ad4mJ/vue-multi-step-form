<template>
  <div id="app">
    <component
      v-on:updateCurrentComponent="updateCurrentComponent"
      v-on:saveOrUpdateDetails="saveOrUpdateDetails"
      v-on:saveOrUpdateAbout="saveOrUpdateAbout"
      v-on:submitApplication="submitApplication"
      :is="currentComponent"
    ></component>

    <button class="btn-toggle toggle-mode" @click="toggleMode">
      Toggle Dark-Mode
    </button>
  </div>
</template>

<script>
import Welcome from "./views/Welcome.vue";
import About from "./views/About.vue";
import Details from "./views/Details.vue";
import Upload from "./views/Upload.vue";
import Success from "./views/Success.vue";

export default {
  name: "App",
  data() {
    return {
      currentComponent: Welcome,
      mode: "light-theme",
      detailsFormData: {},
      aboutFormData: {}
    };
  },
  methods: {
    updateCurrentComponent(component) {
      const componentMap = {
        welcome: Welcome,
        about: About,
        details: Details,
        upload: Upload,
        success: Success
      };
      this.currentComponent = componentMap[component];
    },
    saveOrUpdateDetails(formData) {
      this.detailsFormData = formData;
      this.updateCurrentComponent("about");
    },
    saveOrUpdateAbout(formData) {
      this.aboutFormData = formData;
      this.updateCurrentComponent("upload");
    },
    async submitApplication(files) {
      try {
        let formData = new FormData();
        formData.append("first_name", this.detailsFormData.first_name);
        formData.append("last_name", this.detailsFormData.last_name);
        formData.append("email", this.detailsFormData.email);
        formData.append("phone_number", this.detailsFormData.phone_number);
        formData.append(
          "live_in_uk",
          this.aboutFormData.live_in_uk === "Yes" ? true : false
        );
        formData.append("git_profile", this.aboutFormData.git_profile);
        formData.append("about_you", this.aboutFormData.about_you);
        files.forEach((file, index) => {
          formData.append("file" + (index + 1), file);
        });
        const response = await fetch(
          "https://recruitment-submissions.netsells.co.uk/api/vacancies/javascript-developer/submissions",
          {
            method: "POST",
            body: formData
          }
        );

        if (response.status === 200) {
          this.updateCurrentComponent("success");
        } else {
          //TODO Handle error response
        }
      } catch (error) {
        //TODO Handle error response
      }
    },
    toggleMode() {
      this.mode === "light-theme"
        ? (this.mode = "dark-theme")
        : (this.mode = "light-theme");
      document.body.className = `${this.mode}`;
    }
  }
};
</script>

<style lang="scss">
@import "./assets/styles/main.scss";
</style>
