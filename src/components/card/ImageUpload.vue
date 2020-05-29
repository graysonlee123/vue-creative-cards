<template>
  <div class="row">
    <div class="col-sm-12">
      <h4>Upload Image</h4>
      <div class="form-group">
        <input type="file" class="form-control-file" id="fileUpload" @change="uploadFile" />
      </div>
      <progress value="0" max="100" id="progressBar"></progress>
      <br />
      <img id="image" />
      <button type="button" id="setImageButton" style="display: none;" @click="setImage">Set Image</button>
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
      document.getElementById("setImageButton").style.display = "none";
      
      this.file = e.target.files[0];
      const storageRef = Firebase.storage().ref(
        "user_uploads/" + this.file.name
      );
      const upload = storageRef.put(this.file);

      // Create thumbnail
      const reader = new FileReader();
      reader.readAsDataURL(this.file);

      reader.onload = function(f) {
        document.getElementById("image").src = f.target.result;
      };

      // Progress bar
      upload.on("state_changed", function(snapshot) {
        let progress = (snapshot.bytesTransferred / snapshot.totalBytes) * 100;

        document.getElementById("progressBar").value = progress;

        if (progress === 100) {
          document.getElementById("setImageButton").style.display =
            "inline-block";
        }
      });
    },
    setImage: function() {
      this.$emit("displayImageChanged", this.file.name);
    }
  }
};
</script>

<style scoped>
img {
  max-width: 200px;
}
</style>