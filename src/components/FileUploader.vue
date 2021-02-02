<template>
  <div>
    <div>{{ message }}</div>
    <input type="file" @change="onFileChange" />
  </div>
</template>

<script>
var sha256 = require('js-sha256');

export default {
  data() {
    return {
      message: "SHA256 sample",
    };
  },
  methods: {
    // 選択されたファイルをBinaryで読み出して、sha256を計算する.
    onFileChange: function(event) {
      console.log("onFileChange", event.target.files);
      this.message = '計算中';
      var file = event.target.files[0];
      var reader = new FileReader();
      reader.onload = (event) => {
        var data = event.target.result;
        this.message = sha256(data);
        console.log("encrypted: " + this.message);
      };
      reader.readAsArrayBuffer(file);
    },
  },
};
</script>

