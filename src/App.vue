<template>
  <div id="app">
    <Rvps />
  </div>
</template>

<script>
import Rvps from './components/rvps.vue'
export default {
  name: 'App',
  components: {
    Rvps
  }
}
</script>

<style>
body,
div,
h1,
h2,
h3,
h4,
h5,
h6,
button,
input,
select,
textarea,
span {
  margin: 0;
  padding: 0;
  border: 0;
}

#app {
  display: flex;
  flex-direction: column;
  align-items: center;
}

</style>
