<template>
  <div
    class="tab-pane"
    v-show="active"
    :id="id || title"
    :class="{ active: active }"
  >
    <slot />
  </div>
</template>

<script>
export default {
  name: 'tab-pane',
  props: {
    title: {
      type: String,
      default: '',
      description: 'Tab pane title'
    },
    id: {
      type: String,
      default: null,
      description: 'Tab pane id'
    }
  },
  inject: ['addTab', 'removeTab'],
  data() {
    return {
      active: false
    };
  },
  mounted() {
    this.addTab(this);
  },
  unmounted() {
    if (this.$el && this.$el.parentNode) {
      this.$el.parentNode.removeChild(this.$el);
    }
    this.removeTab(this);
  }
};
</script>

<style></style>
