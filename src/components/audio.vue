<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <el-upload
      ref="elUpload"
      class="upload-demo"
      action="customize"
      multiple
      :limit="1"
      accept=".zip"
      :file-list="fileList"
      :on-change="onchange"
    >
      <div slot="tip" class="el-upload__tip">上传要求：仅支持zip压缩包，小于30MB;</div>
    </el-upload>
    <div class="block" id="block1"></div>
  </div>
</template>

<script>
const Console = console;
import JsZip from "jszip";

export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data() {
    return {
      fileList: [],
      imgs: []
    };
  },
  methods: {
    onchange(file) {
      // var _this = this
      var idx = file.name.lastIndexOf(".");
      var type = file.name.substr(idx + 1);
      if (type === "zip") {
        const isLt2M = file.size / 1024 / 1024 < 30;
        if (!isLt2M) {
          //文件大小超过30M,报错
          this.$message({
            message: "上传文件大小不能超过 30MB!",
            type: "warning"
          });
        } else {
          var new_zip = new JsZip();
          // console.log(new_zip.loadAsync(file.raw))
          new_zip.loadAsync(file.raw).then(function(file) {
            Console.log("zip", Object.values(file.files));
            // mac os zip 多余__MACOSX/ 目录,正常服务器返回的zip没有问题
            for (var key in file.files) {
              // skip mac压缩的文件
              const patt = new RegExp("__MACOSX/");
              //内置函数,判断是否是文件夹
              if (!file.files[key].dir && !patt.test(file.files[key].name)) {
                var base = file.file(file.files[key].name).async("base64");
                base.then(function(res) {
                  Console.log("res", res);
                  var bigAudio = document.createElement("AUDIO");
                  bigAudio.setAttribute("src", `data:audio/wav;base64,${res}`);
                  bigAudio.setAttribute("controls", "controls");
                  var myDiv = document.getElementById("block1"); //获得dom对象
                  myDiv.appendChild(bigAudio);
                });
              }
            }
          });
        }
      }
    },
    changeFile() {}
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
p {
  text-indent: 5em;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.block {
  width: 400px;
  height: 200px;
  border: 1px solid #42b983;
  margin-left: calc(50% - 200px);
}
</style>
