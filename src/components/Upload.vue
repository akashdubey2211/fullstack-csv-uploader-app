<template>
  <div class="input-group mb-3">
    <input type="file" @change="onFileChange" class="form-control" placeholder="upload csv file.." aria-label="Recipient's username" aria-describedby="button-addon2">
    <button @click="onUploadFile" :disabled="!this.selectedFile" class="btn btn-success" type="button" id="button-addon2">Upload</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
    name: "upload-files",
  data() {
    return {
      selectedFile: null,
    };
  },
  methods: {
    onFileChange(e) {
      const selectedFile = e.target.files[0]; // accessing file
      this.selectedFile = selectedFile;
    },
    onUploadFile() {
      const formData = new FormData();
      formData.append("file", this.selectedFile);  // appending file

     // sending file to the backend
      axios
        .post("http://localhost:4000/", formData)
        .then(res => {
          console.log(res);
        })
        .catch(() => {
        //   console.log(err);
        });
    }
  }
};

</script>

<style scoped>
input[type=file] , button {
  width:200px;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

</style>