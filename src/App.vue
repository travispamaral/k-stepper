<template>
  <div id="app">
    <KStepper
      v-model="activeStep"
      :steps="steps"
      @changed="handleChange"
    />
  </div>
</template>

<script>
import Step2 from '@/components/steps/step2'
import Step3 from '@/components/steps/step3'

import KStepper from '@/components/KStepper'
export default {
  name: 'App',
  components: {
    KStepper
  },
  data () {
    return {
      // activeStep: 0,
      steps: [
        {
          title: 'Step 1 title',
          isActive: true,
          content: 'Wow look mah',
          description: 'Lorem ipsum dolor sit amet consectetur adipisicing elit.'
        },
        {
          title: 'Step 2 title',
          component: Step2
        },
        {
          title: 'Step 3 title',
          component: Step3
        }
      ]
    }
  },
  computed: {
    activeStep () {
      return (location.hash && parseInt(location.hash.substring(1))) || 0
    }
  },
  methods: {
    handleChange (state) {
      const newActiveStep = this.steps.findIndex(x => x.title === state.current.title)

      // state.previous.isCompleted = true
      location.hash = newActiveStep
      // this.activeStep = newActiveStep
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: "Roboto", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 700px;
  margin: 50px auto 0;
}

.text-muted {
  color: var(--tblack-45);
}
</style>
