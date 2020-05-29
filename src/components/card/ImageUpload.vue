<template>
  <div class="row">
    <div class="col-sm-12">
      <h4>Upload Image</h4>
      <div class="form-group">
        <input type="file" class="form-control-file" id="fileUpload" @change="uploadFile" />
      </div>
      <br />
      <img id="image" />
      <button type="button" id="setImageButton">Set Image</button>
    </div>
  </div>
</template>

<script>
import Firebase from "firebase";

export default {
  data: function() {
    return {
      file: ""
    };
  },
  methods: {
    uploadFile: function(e) {
      this.file = e.target.files[0];
      const storageRef = Firebase.storage().ref(
        "user_uploads/" + this.file.name
      );
      storageRef.put(this.file);

      const reader = new FileReader();
      reader.readAsDataURL(this.file);

      reader.onload = function(f) {
        document.getElementById("image").src = f.target.result;
      };
    }
  }
};
</script>

<style scoped>
img {
  max-width: 200px;
}
</style>