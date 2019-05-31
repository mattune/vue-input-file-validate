<template>
  <div id="app">
    <vifvInput type="jpg" name="sample" @checkResult="getResult"/>

    <div id="checkResult">
      チェック結果 : <strong id="resultTxt" v-html="formValidate"></strong>
    </div>
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
      formValidate: ''
    }
  },
  methods: {
    getResult(result){
      console.log(result);
    }
  }
}
</script>

<style lang="scss">
#app {
  padding: 100px;
}

#checkResult {
  margin-top: 50px;

  #resultTxt {
    font-size: 2rem;
  }
}
</style>
