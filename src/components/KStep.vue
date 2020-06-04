<template>
  <div
    class="step"
    :class="{ 'is-active': isActive }"
    @click="$emit('change', step)"
  >
    <div class="step-header">
      <div class="step-indicator">
        {{ step }}
      </div>
      <div class="step-title">
        Some Title
      </div>
    </div>
    <div class="step-content">
      <div class="step-inner-content">
        <div
          v-if="description"
          class="description"
        >
          <p class="text-muted mb-0 mt-0">
            <slot name="description">
              {{ description }}
            </slot>
          </p>
        </div>
        <div class="content">
          <slot>{{ content }}</slot>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'KStep',
  props: {
    isActive: {
      type: Boolean,
      default: false,
      required: false
    },
    step: {
      type: Number,
      required: true
    },
    description: {
      type: String,
      default: 'Lorem ipsum dolor sit amet consectetur adipisicing elit.',
      required: false
    },
    content: {
      type: String,
      default: 'Some content here'
    }
  }
}
</script>

<style lang="scss" scoped>
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
      opacity: .5;
      z-index: 1;
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
      max-width: 220px;
    }
    .content {
      flex: 1;
      margin-left: 2rem;
    }
  }
}
</style>
