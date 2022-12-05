<script setup>
 const   product = "Socks";
 const   firstName = "KyuSung";
 const   lastName = "Hwang";
 const   message = "This is the sample test message";
 const   description = "A pair of warm, fuzzy socks";

</script>

<template>
  <div id="app">
    <h2>{{ product }}</h2>
    <h2>{{ product + '?' }}</h2>
    <h2>{{ firstName + ' '  + lastName}}</h2>
    <h2>{{ message.split('').reverse().join('') }}</h2>
    <p> {{ description }}</p>
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
