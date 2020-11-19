<template>
  <div id="app">
    <ClientForm />
  </div>
</template>

<script>
import ClientForm from './components/ClientForm'

export default {
  name: 'App',
  components: {
    ClientForm
  }
}
</script>

<style lang="scss">
  body {
    margin: 0;
    padding: 0;
    background-color: #f5f5f5;
    width: 100%;
    height: 100%;
  }
</style>