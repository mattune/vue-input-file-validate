<template>
  <div class="vifv_input">
    <input type="file" v-on:change="init" :name="name">
    <span class="error_txt" v-html="errorTxt" v-if="errorTxt.length"></span>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    type: String,
    name: String
  },
  data () {
    return {
      checkFile: null,
      originalFile: null,
      errorTxt: ''
    }
  },
  methods:{
    init: function(e){
      e.preventDefault();
      const _this = this;

      _this.checkFile = e.target.files[0];
      _this.checkResult(_this.checkFile);
    },

    checkResult: function(file){
      const _this = this;

      let reader = new FileReader();
      reader.onload = function(){
        _this.checkFileType(reader.result).then(function(values) {
          _this.$emit('checkResult', _this.checkFile);
        });
      }

      reader.readAsArrayBuffer(file);
  　},

    checkFileType: function(target, cb){
      const _this = this;

      return new Promise(function(resolve, reject) {
        const ba = new Uint8Array(target);
        let headerStr = '';
        let headerHex = '';
        for (let i = 0; i < 10; i++) { // 始めの10個分を読む
          headerHex += ba[i].toString(16); // 16進文字列で読む
          headerStr += String.fromCharCode(ba[i]); // 文字列で読む
        }

        // reset
        let fileType = 'unknown';
        _this.errorTxt = '';

        // check
        if (headerHex.indexOf('ffd8') != -1) { // JPGはヘッダーに「ffd8」を含む
          fileType = 'jpg';
        }
        else if (headerStr.indexOf('PNG') != -1) { // PNGはヘッダーに「PNG」を含む
          fileType = 'png';
        }
        else if (headerStr.indexOf('GIF') != -1) { // GIFはヘッダーに「GIF」を含む
          fileType = 'gif';
        }
        else if (headerStr.indexOf('BM') != -1) { // BMPはヘッダーに「BM」を含む
          fileType = 'bmp';
        }
        else if (headerStr.indexOf('OggS') != -1) { // OGGはヘッダーに「OggS」を含む
          fileType = 'ogg';
        }
        else if (headerStr.indexOf('ftyp') != -1) { // MP4はヘッダーに「OggS」を含む
          fileType = 'mp4';
        }
        else {
          _this.errorTxt = '不正なファイル形式です。（拡張子を偽装してる時などに表示）';
        }

        if(fileType != 'unknown' && fileType == _this.type) {
          resolve(fileType);
        }
        else {
          _this.errorTxt = '使用できないファイル形式です。（指定した拡張子以外のファイルの時に表示）';
        }
      });

    }
  }
}
</script>

<style scoped lang="scss">
.vifv_input {
  display: inline-block;

  .error_txt {
    color: red;
    font-size: 1.2rem;
    font-style: italic;
    display: block;
    padding-top: 15px;
  }
}
</style>
