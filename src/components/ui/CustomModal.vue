<template>
  <div class="modal" v-if="isShow" @click.stop="showModal">
    <div @click.stop class="modal__content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'custom-modal',
  props: {
    isShow: {
      type: Boolean,
      default: false,
    },
    student: {
      type: Object,
    },
  },
  methods: {
    showModal() {
      this.$emit('update:is-show', false)
    },
  },
}
</script>

<style scoped>
.modal {
  display: flex;
  inset: 0;
  background: rgba(67, 66, 66, 0.5);
  position: fixed;
}
.modal__content {
  margin: auto;
  border-radius: 8px;
  background: #81d8d0;
  min-width: 30vw;
  min-height: 20vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
