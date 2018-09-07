<template>
  <div class="text-center" id="app">
    <h1>Word Translator</h1>
    <h5>Powered by Vue.js</h5>
    <hr>
    <TranslateForm v-on:formSubmit="translateText"></TranslateForm>
    <TranslateOutput v-text="translatedText"></TranslateOutput>
  </div>
</template>

<script>
import TranslateForm from './components/TranslateForm';
import TranslateOutput from './components/TranslateOutput';

export default {
  name: 'App',
  components: {
    TranslateForm, TranslateOutput
  },
  data: function()  {
    return{
      translatedText:''
    }
  },
  methods:  {
    translateText:function(text, language)  {
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20180822T225228Z.517c5650b14ccef6.f33bb6f2d9b75fc4e4ffff421b5e55c6b8177409&lang='+language+'&text=' + text).then((response) => {
        this.translatedText = response.body.text[0];
      });
    }
  }
}
</script>

<style>
body  {
  background: #fefefe;
}
</style>
