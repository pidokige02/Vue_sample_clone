<template>
  <div id="app">
    <h2>{{ product }}</h2>
    <h2>{{ product + '?' }}</h2>
    <h2>{{ firstName + ' '  + lastName}}</h2>
    <h2>{{ message.split('').reverse().join('') }}</h2>
    <p> {{ description }}</p>
  </div>
</template>

<script>
export default {
  name: 'App',
  data : function () {  // below is valid syntax
  // data() {
    return {
      product: "Socks",  //product value appears in the product in these double curly braces in html files
      firstName: "KyuSung",
      lastName: "Hwang",
      message: "This is the sample test message",
      description : "A pair of warm, fuzzy socks"
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
