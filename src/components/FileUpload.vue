<template>
  <section
    class="upload"
    v-cloak
    @dragover="dragover"
    @dragleave="dragleave"
    @drop="drop"
  >
    <section class="target" for="assetsFieldHandle">
      <svg
        width="20"
        height="20"
        x="0"
        y="0"
        viewBox="0 0 477.867 477.867"
        style="enable-background:new 0 0 512 512"
        xml:space="preserve"
      >
        <g>
          <g>
            <g>
              <path
                d="M324.267,119.467c-9.426,0-17.067-7.641-17.067-17.067V0H102.4C74.123,0,51.2,22.923,51.2,51.2v375.467    c0,28.277,22.923,51.2,51.2,51.2h273.067c28.277,0,51.2-22.923,51.2-51.2v-307.2H324.267z"
                fill="#ffffff"
                data-original="#000000"
                style=""
              />
            </g>
          </g>
          <g>
            <g>
              <polygon
                points="341.333,10.001 341.333,85.333 416.666,85.333   "
                fill="#ffffff"
                data-original="#000000"
                style=""
              />
            </g>
          </g>
        </g>
      </svg>
      <div v-if="file">
        <p>
          {{ type }} Uploaded
          <span class="pointer" @click="remove">
            <svg
              width="15"
              height="15"
              x="0"
              y="0"
              viewBox="0 0 427 427.00131"
              style="enable-background:new 0 0 512 512"
              xml:space="preserve"
              class="warning"
            >
              <g>
                <path
                  d="m232.398438 154.703125c-5.523438 0-10 4.476563-10 10v189c0 5.519531 4.476562 10 10 10 5.523437 0 10-4.480469 10-10v-189c0-5.523437-4.476563-10-10-10zm0 0"
                  fill="none"
                  style=""
                  class=""
                />
                <path
                  xmlns="http://www.w3.org/2000/svg"
                  d="m114.398438 154.703125c-5.523438 0-10 4.476563-10 10v189c0 5.519531 4.476562 10 10 10 5.523437 0 10-4.480469 10-10v-189c0-5.523437-4.476563-10-10-10zm0 0"
                  fill="none"
                  style=""
                  class=""
                />
                <path
                  xmlns="http://www.w3.org/2000/svg"
                  d="m28.398438 127.121094v246.378906c0 14.5625 5.339843 28.238281 14.667968 38.050781 9.285156 9.839844 22.207032 15.425781 35.730469 15.449219h189.203125c13.527344-.023438 26.449219-5.609375 35.730469-15.449219 9.328125-9.8125 14.667969-23.488281 14.667969-38.050781v-246.378906c18.542968-4.921875 30.558593-22.835938 28.078124-41.863282-2.484374-19.023437-18.691406-33.253906-37.878906-33.257812h-51.199218v-12.5c.058593-10.511719-4.097657-20.605469-11.539063-28.03125-7.441406-7.421875-17.550781-11.5546875-28.0625-11.46875h-88.796875c-10.511719-.0859375-20.621094 4.046875-28.0625 11.46875-7.441406 7.425781-11.597656 17.519531-11.539062 28.03125v12.5h-51.199219c-19.1875.003906-35.394531 14.234375-37.878907 33.257812-2.480468 19.027344 9.535157 36.941407 28.078126 41.863282zm239.601562 279.878906h-189.203125c-17.097656 0-30.398437-14.6875-30.398437-33.5v-245.5h250v245.5c0 18.8125-13.300782 33.5-30.398438 33.5zm-158.601562-367.5c-.066407-5.207031 1.980468-10.21875 5.675781-13.894531 3.691406-3.675781 8.714843-5.695313 13.925781-5.605469h88.796875c5.210937-.089844 10.234375 1.929688 13.925781 5.605469 3.695313 3.671875 5.742188 8.6875 5.675782 13.894531v12.5h-128zm-71.199219 32.5h270.398437c9.941406 0 18 8.058594 18 18s-8.058594 18-18 18h-270.398437c-9.941407 0-18-8.058594-18-18s8.058593-18 18-18zm0 0"
                  fill="#000000"
                  data-original="#000000"
                  style=""
                  class=""
                />
                <path
                  xmlns="http://www.w3.org/2000/svg"
                  d="m173.398438 154.703125c-5.523438 0-10 4.476563-10 10v189c0 5.519531 4.476562 10 10 10 5.523437 0 10-4.480469 10-10v-189c0-5.523437-4.476563-10-10-10zm0 0"
                  fill="none"
                  style=""
                  class=""
                />
              </g>
            </svg>
          </span>
        </p>
      </div>
      <div v-else>
        <p class="bold">Upload Your {{ type }}</p>
        <span v-if="required" class="text-primary required">*</span>
        <p>
          <small class="text-grey"
            >Drag and drop or upload your {{ type }} file
            <label for="assetsFieldHandle">
              <span class="text-primary pointer">here</span>
            </label>
          </small>
        </p>
      </div>
      <input type="file" @change="onChange" ref="file" id="assetsFieldHandle" />
    </section>
  </section>
</template>
<script>
export default {
  name: "FileUpload",
  props: {
    type: String,
    required: {
      default: false
    }
  },
  data() {
    return {
      file: null
    };
  },
  methods: {
    onChange() {
      this.file = this.$refs.file.files[0];
      this.$emit("addFile", this.$refs.file.files);
    },
    remove() {
      this.file = "";
      this.$emit("removeFile", this.$refs.file.files);
    },
    dragover(event) {
      event.preventDefault();
      event.currentTarget.classList.add("drag-over");
    },
    dragleave(event) {
      event.currentTarget.classList.remove("drag-over");
    },
    drop(event) {
      event.preventDefault();
      this.$refs.file.files = event.dataTransfer.files;
      this.onChange();
      event.currentTarget.classList.remove("drag-over");
    }
  }
};
</script>
<style scoped lang="scss">
.upload {
  input[type="file"] {
    position: absolute;
    top: -16rem;
    opacity: 0;
    -ms-filter: "progid:DXImageTransform.Microsoft.Alpha(Opacity=0)";
    filter: alpha(opacity=0);
  }
  text-align: center;
  p {
    margin: 0;
  }
  .required {
    position: absolute;
    top: 25px;
    left: 210px;
  }
  &.drag-over {
    opacity: 0.5;
  }
}
section.upload section.target {
  position: relative;
  z-index: 16;
  width: 400px;
  height: 6rem;
  margin: 1rem auto;
  padding: 2.5rem 0 1em 0;
  border: 0.2rem dashed #616778;
  -webkit-transition: color 0.2s ease-out, border-color 0.2s ease-out;
  -moz-transition: color 0.2s ease-out, border-color 0.2s ease-out;
  -o-transition: color 0.2s ease-out, border-color 0.2s ease-out;
  -ms-transition: color 0.2s ease-out, border-color 0.2s ease-out;
  transition: color 0.2s ease-out, border-color 0.2s ease-out;
}
</style>
