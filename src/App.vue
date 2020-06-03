<template>
  <div id="app">
    <KStepper />
  </div>
</template>

<script>
import KStepper from '@/components/KStepper'
export default {
  name: 'App',
  components: {
    KStepper
  }
}
</script>

<style lang="scss">
#app {
  font-family: "Roboto", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 500px;
  margin: 50px auto 0;
}

.text-muted {
  color: var(--tblack-45);
}
</style>
