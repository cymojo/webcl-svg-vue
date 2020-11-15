<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <SvgEyesVanilla></SvgEyesVanilla>
    <SvgEyesVue></SvgEyesVue>
  </div>
</template>

<script>
  import SvgEyesVue from './SvgEyesVue.vue'
  import SvgEyesVanilla from './SvgEyesVanilla.vue'
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  components: {
    SvgEyesVue,
    SvgEyesVanilla
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
  SvgEyesVanilla {
    width: 200px;
  }

SvgEyesVue {
  visibility: hidden;
}
</style>
