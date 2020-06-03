<template>
  <div class="k-stepper">
    <KStep
      v-for="s in steps"
      :key="s"
      :step="s"
      :is-active="active === s"
      @change="stepNumber => active = stepNumber"
    />
  </div>
</template>

<script>
import KStep from './KStep'
export default {
  name: 'KStepper',
  components: { KStep },
  data () {
    return {
      active: 1,
      steps: 4
    }
  }
}
</script>

<style lang="scss" scoped>
.k-stepper {
  --indicatorSize: 1.5rem;
  --contentLeftMargin: var(--spacing-sm);
  width: 100%;
}
</style>
