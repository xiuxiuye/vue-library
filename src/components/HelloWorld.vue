<template>
  <div class="hello">
      <h1>hello component div</h1>
      <css-scoped class="TextColor1" style="color:yellow"></css-scoped>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
    }
  },
  components: {
    'css-scoped': ()=>import('./CssScoped.vue')
  },
  methods: {
   
  }
}
</script>
<style scoped>
.hello{
  background-color: chocolate;
  padding: 10px;
}
h1{
  color: green;
}
.TextColor1{
  color: blue
}
</style>
