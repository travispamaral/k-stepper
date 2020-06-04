<template>
  <div class="k-stepper">
    <div
      v-for="(step, idx) in steps"
      :key="idx"
      class="step"
      :class="{ 'is-active': idx === active }"
      @click="handleChange(step, idx, active)"
    >
      <div class="step-header">
        <div
          :class="{ 'is-completed': step.isCompleted }"
          class="step-indicator"
          :data-step="idx + 1"
        />
        <div class="step-title">
          {{ step.title }}
        </div>
      </div>
      <div class="step-content">
        <div class="step-inner-content">
          <div class="description">
            <p class="text-muted mb-0 mt-0">
              <slot name="description">
                {{ step.description }}
              </slot>
            </p>
          </div>
          <div class="content">
            {{ step.content }}
            <component
              :is="step.component"
              v-if="step.component"
            />
            <slot v-else>
              {{ step.content }}
            </slot>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'KStepper',
  // v-model
  model: {
    prop: 'value',
    event: 'input'
  },
  props: {
    steps: {
      type: Array,
      required: true
    },
    value: {
      type: Number,
      default: 1
    }
  },
  data () {
    return {
      active: this.value
        ? this.value
        : 0
    }
  },
  methods: {
    handleChange (step, idx, previousIdx) {
      this.active = idx
      this.$emit('changed', {
        current: step,
        previous: this.steps[previousIdx]
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.k-stepper {
  --indicatorSize: 1.5rem;
  --contentLeftMargin: var(--spacing-sm);
  width: 100%;
  .step {
    position: relative;
    padding-bottom: 1.5rem;
    &:last-of-type:before {
      display: none;
    }
    &:before {
      display: block;
      position: absolute;
      top: var(--indicatorSize);
      // center line (indicator circle / 2 - 1/2 width of line)
      left: calc(var(--indicatorSize) / 2 - .5px);
      width: 1px;
      height: calc(100% - var(--indicatorSize));
      background-color: var(--tblack-10);
      content: '';
      z-index: -1;
    }
    &.is-active {
      .step-header .step-indicator {
        opacity: 1;
      }
      .step-content {
        max-height: 500px;
        height: auto;
        transition: max-height 1s ease-in-out;
      }
    }
    .step-header {
      display: flex;
      align-items: center;
      cursor: pointer;
      .step-indicator {
        display: flex;
        justify-content: center;
        align-items: center;
        width: var(--indicatorSize);
        height: var(--indicatorSize);
        border-radius: 50%;
        color: var(--twhite-1);
        background-color: var(--blue-base);
        background-repeat: no-repeat;
        background-position: center;
        opacity: .5;
        z-index: 1;
        &:before { content: attr(data-step);}
        &.is-completed {
          background-image: url('data:image/svg+xml;charset=US-ASCII,%3Csvg%20width%3D%2213%22%20height%3D%2211%22%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%3E%0A%20%20%3Cpath%20d%3D%22M3.65625%208.125L11.074423.70682704c.3903698-.3903698%201.0270392-.38661482%201.4157789.00212488l-.1991538-.19915384c.3915433.39154333.3980686%201.0198352.006652%201.41125181L4.3585499%209.8602001c-.38786953.3878695-1.01402972.3905701-1.40726168-.0026619L.70496178%207.6112118c-.38933964-.3893397-.38474956-1.025174.00399014-1.4139137l-.19915384.1991538c.39154333-.3915433%201.02761248-.3902913%201.41397791-.0039259L3.65625%208.125z%22%20fill%3D%22%23FFF%22%20stroke%3D%22%23FFF%22%20stroke-width%3D%22.5%22%20fill-rule%3D%22evenodd%22/%3E%0A%3C/svg%3E%0A');
          &:before { content: ''; }
        }
      }
      .step-title {
        margin-left: var(--contentLeftMargin);
      }
    }
    .step-content {
      flex: 1;
      max-height: 0;
      margin-left: calc(var(--indicatorSize) + var(--contentLeftMargin));
      overflow: hidden;
      transition: max-height 1s cubic-bezier(0, 1, 0, 1);
      .step-inner-content {
        display: flex;
        padding-top: 1rem;
      }
      .description {
        width: 300px;
      }
      .content {
        flex: 1;
        margin-left: 2rem;
      }
    }
  }
}
</style>
