<template>
  <div id="app">
    <form action="#">
      <vifvInput checkType="png,jpg,gif" name="sample" required @checkResult="getResult"/>
      <button id="btnSubmit" v-bind:disabled="checkDisabled">送信する</button>
    </form>
  </div>
</template>

<script>
import vifvInput from './components/vifv-input.vue'

export default {
  name: 'app',
  components: {
    vifvInput
  },
  data () {
    return {
      checkDisabled: true
    }
  },
  methods: {
    getResult(result){
      // -----------------------
      // この中は自由に処理してください
      // -----------------------
      console.log(result);
      // とりあえずファイル選択したFile情報を返している
      // エラーの時はnull

      if(result) {
        this.checkDisabled = false;
      }
      else {
        this.checkDisabled = true;
      }
    }
  }
}
</script>

<style lang="scss">
#app {
  padding: 100px;
}

#btnSubmit {
  display: block;
  margin-top: 50px;
  border: 1px solid #000;
  border-radius: 10px;
  padding: 20px;
  cursor: pointer;

  &:disabled {
    background-color: #999;
    cursor: not-allowed;
  }
}
</style>
