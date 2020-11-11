<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <svg-eyes-vanilla></svg-eyes-vanilla>
    <svg-eyes-vue></svg-eyes-vue>
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
  svg-eyes-vanilla {
    width: 200px;
  }
</style>
